---
title: "Linux Client on Windows Domain"
weight: 45
pre: "9. "
---

{{< youtube uyie_GWK2zw >}}

<!-- dQUitxwsUws -->

#### Resources

* [Join in Active Directory Domain](https://www.server-world.info/en/note?os=Ubuntu_20.04&p=realmd) from Server-World
* [How to Join Ubuntu 18.04 / Debian 10 To Active Directory (AD) Domain](https://computingforgeeks.com/join-ubuntu-debian-to-active-directory-ad-domain/) from Computingforgeeks

#### Video Transcript

In the following two videos, we'll look at how to enable interoperability between our Windows- and Linux-based systems. In many organizations today, you'll have a mix of many different operating systems, so it is very helpful to understand how to integrate them together in a single directory service.

In this video, I'll show you how to add an Ubuntu VM to a Windows Active Directory Domain. This is by far the most common use-case for interoperability, and has been used by many organizations including K-State. For most users, Windows Active Directory provides a great set of features for Windows-based systems, and it is simple to integrate Linux and Mac clients into that environment.

For this example, I'm using the Windows 2019 server set up as defined in Lab 4's assignment. I've reconfigured the domain to have the fully qualified domain name `ad.cis527russfeld.cs.ksu.edu` for this example, as you would in a real environment. This is due to the fact that many Linux packages do not accept the `.local` top-level domain I used in the previous video as an example.

For the client, I am using a copy of my Ubuntu 20.04 VM labelled **CLIENT** from Lab 3. For this assignment, you'll use that same VM, but restored to a snapshot taken before it was configured as a client for OpenLDAP. Remember that you'll need create this snapshot before you start the Lab 4 assignment, or else you may need to create a new VM for this activity.

Finally, I've found there really isn't a great guide for doing this online, but I'm generally following the instructions in the Server-World guide linked below this video. I'll do my best to clarify what parts are important and what parts I leave out and why.

First, as with any client I wish to add to a domain, I'll need to set a static DNS entry to point to the domain controller itself. For the second entry, I'll just use the VMware router as always. Once I've done that, I'll disable and enable the network connection so that my changes take effect. 

Then, I'll need to install the `realmd` package. This package allows us to interface with Active Directory Domain servers.

```bash
sudo apt update
sudo apt install realmd
```

The instructions found online typically have you install a large number of packages at this step, but don't do a good job of describing what they are used for. Thankfully, Ubuntu 20.04 includes a special program called `packagekit` by default, which allows us to automatically install the packages we need as we need them. So, we'll start by just installing `realmd` and going from there.

Once we have `realmd` installed, we can use it to query our Active Directory domain using the `realm discover` command:

```bash
realm discover ad.cis527russfeld.cs.ksu.edu
```

If that command works correctly, you should see output giving information about the Active Directory Domain we just queried. However, if you get an error at this step, that usually means that something isn't working correctly. In that case, double-check that you have properly set your DNS entries, and that you can ping your Windows 2019 server using both the IP address and the Active Directory Domain name. You'll need to be able to use DNS to resolve that domain name in order for this system to join the domain.

Once we are ready to join the domain, we can simply using the `sudo realm join` command.

```bash
sudo realm join ad.cis527russfeld.cs.ksu.edu
```

Once we enter that command, we'll be prompted for the password for the `Administrator` account. This is the `Administrator` account of our Active Directory domain, so we'll have to provide the correct password here.

Here's where the cool part happens. The `realmd` program is smart enough to know what packages we need in order to interface with an Active Directory domain, and because we have `packagekit` installed on Ubuntu 20.04 by default, the `realmd` command can automatically install those packages when we use the `realm join` command. So, we don't have to worry about remembering to install all of these packages manually - it is done for us automatically! Very handy!

Ok, now that we have joined the domain, we can see if we can get information about an Active Directory user account using the `id` command:

```bash
id russfeld@ad.cis527russfeld.cs.ksu.edu
```

If everything is working correctly, you should see some information about that user printed to the screen. If not, you'll need to do some troubleshooting.

Now, we can even log in as that user using the `su`, or "switch user" command:

```bash
su russfeld@ad.cis527russfeld.cs.ksu.edu
```

There we go! We are now logged in to this system as one of our Active Directory users. However, there are couple of things we can do to improve this experience. First, notice that we have to enter our fully qualified domain name for our Active Directory domain to log in. That can get really annoying, espeically with a long domain like ours. Also, what if we try to check our home directory:

```bash
cd ~/
```

We find out that this user doesn't even have a home directory to store files in. That's no good!

So, let's log out of this user and try to fix these issues.

```bash
exit
```

First, let's change a setting so that we don't have to enter the full Active Directory Domain name each time we want to log in as one of those users. To do that, we'll edit the `sssd` configuration file. The `sssd` package helps provide access to authentication resources across many different sources. 

```bash
sudo nano /etc/sssd/sssd.conf
```

In that file, we'll see a line like the following:

```tex
use_fully_qualified_names = True
```

We'll simply set that setting to `False` and then save the file.

```tex
use_fully_qualified_names = False
```

Finally, we can restart the `sssd` daemon to load the new settings.

```bash
sudo systemctl restart sssd
```

Now, we can use the `id` command with just the username:

```bash
id russfeld
```

and we should get the correct info. We can even use that username to log in to the system using the `su` command.

```bash
su russfeld
exit
```

Yay! Now, let's tackle the creation of home directories. This is handled by the Pluggable Authentication Modules, or PAM, framework. There are many ways to do this, including editing a config file manually. However, there is a quick and easy way to do this as well, using the `pam-auth-update` command:

```bash
sudo pam-auth-update
```

In the menu, press the <kbd>SPACE</kbd> key to enable the "Create home directory on login" option, then press <kbd>ENTER</kbd> to save the changes.

There we go! Now, when we log in as our domain user, it will automatically create a home directory for us:

```bash
su russfeld
cd ~/
pwd
```

Awesome! Now, one interesting thing to discuss at this point is the fact that many online tutorials require us to install the `oddjob` and `oddjob-mkhomedir` packages. As far as I can tell, these are only required if we are using `selinux` instead of `apparmor` to protect our system. Since we aren't doing that, we'll just leave this out for now. However, if you do decide to use `selinux` on your system, you may have to do some additional configuration in order for your home directories to be properly created.

Ok, the last thing we may want to tackle on this system is the ability for our domain users to log on graphically. In previous versions of Ubuntu, this required a bit more configuration. However, in Ubuntu 20.04, all we have to do is restart the system to reload a few of the changes we just made. Then, we can click the "Not listed?" option at the bottom of the login window, and enter our domain username and password.

Voila! That's all it takes to log on graphically using an Active Directory domain user account on Ubuntu 20.04. The process has gotten much simpler over the years, to the point where it isn't that much more difficult than adding a Windows 10 client to a domain. 
