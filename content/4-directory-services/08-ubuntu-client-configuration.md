---
title: "Ubuntu Client Configuration"
weight: 40
pre: "8. "
---

{{< youtube jGRXpQekHZc >}}

#### Resources

* [Configure LDAP Client on Ubuntu 16.04 / Debian 8](https://www.itzgeek.com/how-tos/linux/ubuntu-how-tos/configure-ldap-client-on-ubuntu-16-04-debian-8.html) on ITz Geek (should work on 18.04 as well)
* [Configure LDAP Client](https://www.server-world.info/en/note?os=Ubuntu_18.04&p=openldap&f=3) from Server-World
* [OpenLDAP Server](https://help.ubuntu.com/lts/serverguide/openldap-server.html.en) on Ubuntu Server Guide (look for the LDAP Authentication section)
* [How to Configure Ubuntu as an LDAP Client](https://askubuntu.com/questions/127389/how-to-configure-ubuntu-as-an-ldap-client) from AskUbuntu (possible solution to graphical login)

#### Video Transcript

Once we've set up and configured our OpenLDAP server on Linux, we can configure another VM to act as an LDAP client and use that server for authentication. Unfortunately, there are not many good guides online for this process, so I'll walk through most of the process in this video, discussing the process while I do so.

In general, I'm going to follow the first guide linked below this video, which is from ITz Geek. The second guide, from Server-World, is very similar and should work as well.

First, I'll need to install a few packages:

```bash
sudo apt update
sudo apt install libnss-ldap libpam-ldap ldap-utils nscd
```

When you are installing those packages, you'll need to configure your LDAP settings. For the server URL, you'll need to input the IP address of the LDAP server. For my setup, that would be `ldap://192.168.40.41`. I'll also need the distinguished name, which is the base DN from your LDAP server. So, my example would be `dc=cis527,dc=local`. Our server is only configured for LDAP version 3, so we'll have to use that version.

Since we would like to allow users to update their LDAP passwords, we'll need to make the local root account a database admin, so I'll select `<Yes>` for that option. Our LDAP server does not require authentication, so we can select `<No>` there. Finally, we'll need to input the LDAP admin account information to allow password changes. In my setup, the account is `cn=admin,dc=cis527,dc=local` and the password is the one I configured in the previous video.

That should be enough for the installation process to complete. Next, we'll need to configure the system to use LDAP accounts for authentication. There are two files we need to edit. First, we'll edit the `nsswitch` configuration file:

```bash
sudo nano /etc/nsswitch.conf
```

We'll add `ldap` to the end of the lines for `passwd`, `group`, and `shadow`. Some guides have you place `ldap` before the existing entries, but this could cause your system to lock up at boot time if the LDAP server cannot be contacted.

Next, we'll edit the `common-session` file:

```bash
sudo nano /etc/pam.d/common-session
```

At the bottom of the file, we'll add the following line:

```bash
session required  pam_mkhomedir.so skel=/etc/skel umask=077
```

That line will tell the system to create a home directory for the user if one doesn't exist, and will copy a skeleton home directory for starters. As a sidenote, if you want to customize any of the files that your users would receive in their home folders, you could edit the files present in /etc/skel. This could even be done using Puppet!

Finally, you'll need to restart the Name Service Cache Daemon:

```bash
sudo systemctl restart nscd
```

Now, you can check to see if it worked. The easiest way is to query the `passwd` database using the `getent` command:

```bash
getent passwd russfeld
```

If it returns a result, you should be able to log in as that user using the `su` command:

```bash
su russfeld
```

Now, at this point, I should point out one very important impact of how our system is configured. I am logged in as an LDAP user, but notice that if I try to log in as root, I'm able to use `sudo` without any additional configuration! **Yikes!**

How did that happen? It actually is due to a setting in our `sudoers` file that is present by default on all Ubuntu systems. Let's take a look at that file:

```bash
sudo visudo
```

If we look through that file, we'll find a line that says members of the `admin` group may gain root privileges. In fact, that's exactly what happened! Just because we chose to name our group `admin` on the LDAP server, our users would automatically gain `sudo` access on any system they log into. The same would happen for a group named `sudo` as well. So, it is very important to make sure your groups on your LDAP server use unique names, otherwise you may inadvertently create a major security hole in your systems.

To test the graphical login, you'll need to fully reboot your computer. Once that is done, you can click the "Not listed?" option at the bottom of the list of users, then enter the credentials for your LDAP user to log in. If everything is configured correctly, it should let you log in directly to the system.

You have now successfully configured your system to allow Ubuntu to use LDAP servers for user accounts. This should be enough information to help you complete that section of Lab 4. As always, if you have any questions, feel free to post in the course discussion forums on Canvas. Good luck!
