---
title: "Windows Client on Linux Domain"
weight: 50
pre: "10. "
---

{{% notice note %}}

_This portion is no longer part of the Lab 4 assignment, but I left it here because it is interesting to know that it can be done. --Russ_

{{% /notice %}}

{{< youtube t3ESN_EXGGw >}}

#### Resources

* [How to Configure Ubuntu Linux Server as a Domain Controller with Samba-tool](https://www.techrepublic.com/article/how-to-configure-ubuntu-linux-server-as-a-domain-controller-with-samba-tool/) by Jack Wallen on TechRepublic
* [Samba Not Starting on Ubuntu Server 16.10](https://unix.stackexchange.com/questions/341226/samba-not-starting-on-ubuntu-server-16-10) from StackExchange
* [How to Disable Systemd-resolved in Ubuntu](https://askubuntu.com/questions/907246/how-to-disable-systemd-resolved-in-ubuntu) from AskUbuntu

#### Video Transcript

In this video, I'll show you how to set up an Ubuntu VM to act as a Windows Active Directory Domain Controller using Samba. Unfortunately, at this time it is not straightforward at all to use OpenLDAP as the server, hence the decision to use Samba instead. This is a much more complicated process than adding Ubuntu as a client to an existing Active Directory Domain, but I feel that it is important to see that it is indeed possible. This is helpful if your organization is primarily Linux-based, but you wish to include a few Windows clients on the network as well.

For this example, I'm using the Ubuntu VM labelled **Client** from earlier in this lab. I've created a snapshot to store the work done previously to add it to an OpenLDAP domain, but now I've restored the snapshot labelled "Before Lab 4" and will use that snapshot to create a Samba server. The reason I am doing this on the VM labelled **Client** and not the one labelled **Server** is because the Samba installation will directly conflict with Bind9, OpenLDAP, and many other tools we've already installed on the server. So, this allows us to avoid any conflicts with those tools.

For the client, I have restored my Windows 10 VM to a snapshot taken before it was added to my Active Directory Domain. Remember that you'll need to create this snapshot before you start the Lab 4 assignment, or else you may need to create a new VM for this activity.

Finally, I'll generally be following the great guide by Jack Wallen that is linked in the resources section below this video, but I'll be making a few minor changes to match our environment and clarifying a few things that he leaves out.

Before we begin, we'll need to set a static IP on this system, since it will be acting as a server. I'm going to use the IP ending in `45` in my local subnet. For the DNS entries, we'll also need to set the first entry to be this system itself, just like we did with the Windows Domain Controller. The second DNS entry can be the VMware router or any other valid DNS server.

First, we'll need to install Samba as well as a few supporting tools:

```bash
sudo apt update
sudo apt install samba libpam-winbind smbclient
```

This will install many supporting packages as well.

Next, we need to make a few edits to our `hosts` file as well as update our hostname. This will help Samba find the correct settings as we configure it in a later step. First, let's edit the `hosts` file:

```bash
sudo nano /etc/hosts
```

I'll need to add or edit a few entries at the top of this file. Here's what mine currently looks like:

```
127.0.0.1       localhost.localdomain
127.0.1.1       dc
192.168.40.41   localhost
192.168.40.41   smbrussfeld.cis527.cs.ksu.edu       smbrussfeld
192.168.40.41   dc.smbrussfeld.cis527.cs.ksu.edu    dc
```

The first line is updated to be `localhost.localdomain`, just to make it clear that that IP address is for the loopback adapter. The second line gives the new hostname for this system. In this case, I'm calling it `dc` for domain controller. The third line redirects the `localhost` domain name to the external IP address. Finally, the fourth and fifth lines give the name of the domain as well as the fully qualified domain name for this system, respectively.

To go along with this change, we'll edit the `hostname` file as well:

```bash
sudo nano /etc/hostname
```

It should now be the same as the hostname used in the `hosts` file:

```
dc
```

Finally, we'll need to restart the computer for these changes to take effect.

Once it has restarted, we'll need to remove any existing Samba configuration files and database files.

Thankfully, there are some great commands for finding the location of those files. First, you can find the location of the config file using this command:

```bash
smbd -b | grep "CONFIGFILE"
```

It is usually at `/etc/samba/smb.conf`. So, to delete it, you'll use:

```bash
sudo rm -f /etc/samba/smb.conf
```

Next, you can find the locations of all database files using this command:

```bash
smbd -b | egrep "LOCKDIR|STATEDIR|CACHEDIR|PRIVATE_DIR"
```

It should give you four different directory paths. So, for each of those directories, you'll need to enter that directory, then delete all files with the `.tdb` and `.ldb` file extensions. So, for the first one, you could use these commands:

```
cd /var/run/samba
sudo rm -f *.tdb *.ldb
```

Repeat that process for the other three directories to make sure they are all clear.

Once that is done, it is time to create our new domain. We'll use the `samba-tool` command to do this in interactive mode:

```bash
sudo samba-tool domain provision --use-rfc2307 --interactive
```

First, it will ask you for the realm. For this example, I'll use the name `smbrussfeld.cis527.cs.ksu.edu`. Following that, it should ask you for the NetBIOS name of your domain. The default should be `smbrussfeld`, which is fine. You can also accept the defaults of `dc` for the server role, and `SAMBA_INTERNAL` for the DNS backend. For the DNS forwarder address, you can use the VMware router's IP address, or any other valid DNS server address from Lab 3. Finally, you'll need to enter a password for the Administrator account. I'll use the same password as always.

Once you've entered that information, your domain will be configured. Now, we'll need to add a user to Samba and enable it using the following commands:

```bash
sudo smbpasswd -a <username>
sudo smbpasswd -e <username>
```

Next, we'll need to disable the `systemd-resolved` service. This service is installed by default on Ubuntu 18.04, and is responsible for caching local DNS queries. However, since it binds to port 53, it will prevent our Samba server from binding to that port. To disable it, we'll use the following commands:

```bash
sudo systemctl disable systemd-resolved
sudo systemctl stop systemd-resolved
```

We'll also need to disable the existing Samba services, and enable the Samba Domain Controller service:

```bash
sudo systemctl disable nmbd
sudo systemctl stop nmbd
sudo systemctl disable smbd
sudo systemctl stop smbd
sudo systemctl unmask samba-ad-dc
sudo systemctl enable samba-ad-dc
sudo systemctl start samba-ad-dc
```

Lastly, we'll need to replace any existing Kerberos configuration file with the one created by Samba. So, you'll perform these commands to delete the existing file (if any) and create a symbolic link to the one from Samba.

```bash
sudo mv /etc/krb5.conf /etc/krb5.conf.orig
​sudo ln -sf /var/lib/samba/private/krb5.conf /etc/krb5.conf
```

If you get an error from the first command, you can safely ignore it.

Finally, if everything is configured correctly, we can query our domain using the `smbclient` command:

```bash
smbclient -L localhost -U%
```

Hopefully you should get output from that command giving information about your domain. If not, you'll probably need to review the Samba log file stored in `/var/log/samba/log.samba` to see what the error is.

If everything is working correctly, you can then add your Windows 10 VM to the domain. First, as with any client I wish to add to a domain, I'll need to set a static DNS entry to point to the domain controller itself. For the second entry, I'll just use the VMware router as always. Then, I can add it to the domain following the instructions in the earlier video.

After a reboot, it should allow you to log in as the domain user created earlier.

It is quite a process, but hopefully this demonstrates what it takes to create an Active Directory Domain using Samba. I highly recommend that you try this process at least once, even if you don't plan on completing it as part of Lab 4, just to see how it all works together.
