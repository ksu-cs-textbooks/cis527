---
title: "Ubuntu Client Configuration"
weight: 40
pre: "8. "
---

{{< youtube sTDsiX90KCQ >}}

<!-- 9aOZ-qy_KKc -->

{{% notice note %}}

See the transcript below for an updated version of the `ldapwhoami` command. 

{{% /notice %}}


#### Resources

* [SSSD and LDAP](https://ubuntu.com/server/docs/ldap-and-transport-layer-security-tls) on Ubuntu Server Guide

#### Video Transcript

Once we've set up and configured our OpenLDAP server on Linux, we can configure another VM to act as an LDAP client and use that server for authentication. Thankfully, now that Ubuntu 20.04 uses SSSD, this process is pretty simple. 

For the most part, we'll be following the instructions in the Ubuntu Server Guide page linked below this video. It is a pretty in-depth overview of how to configure SSSD to use LDAP for authentication. In fact, if you've done the Windows portions of this assignment already, you'll be familiar with several of these steps.

First, we'll need to install a couple of packages on this system to allow us to interact with LDAP systems via SSSD:

```bash
sudo apt update
sudo apt install sssd-ldap ldap-utils
```

Next, we'll need to get a copy of our certificate authority, or CA, certificate from our Ubuntu 20.04 VM labelled **SERVER**. If we followed the instructions in the previous video correctly, we should have created a copy of that file in the home directory of the `cis527` user on our server. 

If not, you can do so by logging on to the **SERVER** VM as `cis527` and using the following command:

```bash
cp /usr/local/share/ca-certificates/mycacert.crt ~/
```

Then, from the **CLIENT** VM, we can use `scp` to copy that file using SSH. Hopefully you were able to get the SSH portion of the lab set up and working correctly. If not, you may have to copy this from the **SERVER** VM to your host system, and then from your host system back to the **CLIENT** VM. To copy the file using `scp`, use a command similar to the following

```bash
scp -P 22222 cis527@192.168.40.41:~/mycacert.crt ~/
```

Let's break that command down. First, the `-P 22222` tells us the we are using port 22222 to connect to the system, which is how it was configured in Lab 3. Then, we have `cis527@`, which is the username we'd like to use on the remote system, followed by `192.168.40.41`, which is the IP address of our **SERVER** VM. Next, there is a colon, and a file path, which is `~/mycacert.crt`, which is the path to the certificate file on the **SERVER** VM. Finally, we have a space, and another path `~/` showing where we'd like to place the file on our **CLIENT** VM. 

Of course, if you want to learn more about SSH and SCP, check out the video in the Extras section for more information.

Once we have a copy of the certificate on our **CLIENT** VM, we can install it using the following commands:

```bash
sudo cp ~/mycacert.crt /usr/local/share/ca-certificates/
sudo update-ca-certificates
```

If that command works correctly, it should tell us that it has added 1 certificate to our list. That means that our **CLIENT** VM now includes our own self-signed CA in its list of trusted CA certificates. That's what we want!

---

Next, we'll need to create an SSSD configuration file. Unfortunately, unlike the example we'll see later with Windows and Active Directory, we'll have to create this one manually. Here's an example of what that would look like. First, we'll open the file:

```bash
sudo nano /etc/sssd/sssd.conf
```

and then put the following contents inside of it:

```tex
[sssd]
config_file_version = 2
domains = ldap.cis527russfeld.cs.ksu.edu

[domain/ldap.cis527russfeld.cs.ksu.edu]
id_provider = ldap
auth_provider = ldap
ldap_uri = ldap://ldap.cis527russfeld.cs.ksu.edu
cache_credentials = True
ldap_search_base = dc=ldap,dc=cis527russfeld,dc=cs,dc=ksu,dc=edu
```

Notice that we've customized this file to match our LDAP configuration information from the previous video. 

Also, we must make sure that that file is owned by `root:root` and only the user has permission to access that file:

```bash
sudo chown root:root /etc/sssd/sssd.conf
sudo chmod 600 /etc/sssd/sssd.conf
```

Finally, we can restart the SSSD service to load the new settings:

```bash
sudo systemctl restart sssd
```

If this command returns an error, it usually either means that there is a typo in the `sssd.conf` file created earlier, or that the file's permissions are incorrect. So, make sure you double-check that if you run into an error at this point.

Now, let's tackle the creation of home directories. This is handled by the Pluggable Authentication Modules, or PAM, framework. There are many ways to do this, including editing a config file manually. However, there is a quick and easy way to do this as well, using the `pam-auth-update` command:

```bash
sudo pam-auth-update
```

In the menu, press the <kbd>SPACE</kbd> key to enable the "Create home directory on login" option, then press <kbd>ENTER</kbd> to save the changes.

Finally, we can do some testing to make sure that things are working correctly. First, we'll need to be able to access our LDAP server using its DNS name, so we can test that using dig:

```bash
dig ldap.cis527russfeld.cs.ksu.edu
```

Hopefully you were able to get your LDAP server working in the previous lab. If not, you may load some of the model solution files from Lab 3 provided on Canvas to get this part working. 

Next, we'll make sure we can access the LDAP server

```bash
ldapwhoami -x -H ldap.cis527russfeld.cs.ksu.edu
```

This command should return `anonymous`. If not, your **CLIENT** VM is having trouble contacting your **SERVER** VM or the LDAP server itself. In that case, you may want to check your firewall configuration - did you remember to allow the correct ports for LDAP? 

Once that command works, we can try it again using TLS by adding `-ZZ` to the command:

```bash
ldapwhoami -x -ZZ -H ldap.cis527russfeld.cs.ksu.edu
```

Hopefully this command should return `anonymous` just like it did  previously. If not, there is probably a configuration issue with your TLS certificates that you'll need to resolve before moving on.

Finally, if everything looks like it is working, we can try to load information about one of our LDAP users using the `getent` command:

```bash
getent passwd russfeld
```

This command should return information about the user we created on our LDAP server. If not, then we may need to check the settings in our `sssd.conf` file to make sure the LDAP information is correct. 

Thankfully, if that worked, we can try to log on to the system as that user using the `su` command:

```bash
su russfeld
```

It works! We can even go to our home directory and see that it was created for us:

```bash
cd ~/
pwd
```

Now, at this point, I should point out one very important impact of how our system is configured. I am logged in as an LDAP user, but notice that if I try to log in as root, I'm able to use `sudo` without any additional configuration! **Yikes!**

How did that happen? It actually is due to a setting in our `sudoers` file that is present by default on all Ubuntu systems. Let's take a look at that file:

```bash
sudo visudo
```

If we look through that file, we'll find a line that says members of the `admin` group may gain root privileges. In fact, that's exactly what happened! Just because we chose to name our group `admin` on the LDAP server, our users would automatically gain `sudo` access on any system they log into. The same would happen for a group named `sudo` as well. So, it is very important to make sure your groups on your LDAP server use unique names, otherwise you may inadvertently create a major security hole in your systems.

To test the graphical login, you'll need to fully reboot your computer. Once that is done, you can click the "Not listed?" option at the bottom of the list of users, then enter the credentials for your LDAP user to log in. If everything is configured correctly, it should let you log in directly to the system.

You have now successfully configured your system to allow Ubuntu to use LDAP servers for user accounts. This should be enough information to help you complete that section of Lab 4. As always, if you have any questions, feel free to post in the course discussion forums on Canvas. Good luck!
