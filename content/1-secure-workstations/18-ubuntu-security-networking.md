---
title: "Ubuntu Security & Networking"
weight: 90
pre: "18. "
---

{{< youtube pEDxbeTz0z0 >}}

#### Resources

* **[Slides]({{% relref "/1-secure-workstations/18-ubuntu-security-networking-slides.md"  %}})**
* [Networking, Web & Email](https://help.ubuntu.com/lts/ubuntu-help/net.html) from Ubuntu
* [Networking](https://help.ubuntu.com/lts/serverguide/networking.html) from Ubuntu Server Guide
* [Internet and Networking](https://help.ubuntu.com/community/InternetAndNetworking) from Ubuntu
* [UFW (Uncomplicated Firewall)](https://help.ubuntu.com/community/UFW) from Ubuntu
* [GUFW (Graphical Interface for UFW)](https://help.ubuntu.com/community/Gufw) from Ubuntu

#### Video Script

In this last video on Ubuntu, we'll discuss some important security and networking details needed to finish getting your VMs set up and configured properly.

First, let's talk about security. Whenever you install a new operating system, there are 4 major steps you should always perform before doing just about anything else on the system. Those steps are:

1. **Configure User Accounts & Passwords** - at the very least, make sure you have at least one user account with a secure password added to the `sudo` group to perform administrative tasks. Most other users should have standard accounts without sudo access. You may also add this system to an LDAP directory to get additional user accounts. We'll discuss that in detail in Module 4.
1. **Configure the Firewall** - Ubuntu ships with a firewall installed, but by default it is not configured or enabled. To configure the firewall, I recommend installing the `gufw` tool as a graphical interface for the Ubuntu Uncomplicated Firewall (UFW). Once that tool is installed, you can enable the firewall with a single click.
1. **Install Antivirus Software** - All computers should still run some form of antivirus software. Ubuntu does not provide any by default, but it is very easy to install the ClamAV scanner. It is an open source antivirus scanner, and is recommended for use on all Linux systems.
2. **Install All System Updates** - You should also install all available system updates for your operating system. This makes sure you have patches against the latest known flaws and attacks. Ubuntu has the ability to install updates automatically, but it must be configured. You can search for the Software & Updates program after clicking the Activities button. Once there, look at the Updates tab to configure automatic updates. You can always use Synaptic or apt to make sure all packages are the latest version.

Let's take a quick look at the firewall, since you'll need to allow an application through the firewall. You can find it by searching for "firewall" once you have installed `gufw`. Lab 1 directs you to install the Apache 2 web server. You'll need to allow it through the firewall somehow. I won't show you how in this video, but I encourage you to review the links in the resources section below the video for documentation showing how to accomplish this task. There are several ways to do it.

To test your firewall configuration, you can use your Windows virtual machine created as part of Lab 1. First, make sure they are both on the same network segment in VMware by looking at the hardware configuration for each virtual machine. Then, you'll need to get the IP address of the Ubuntu computer. There are several ways to do this, but one of the simplest is to go to the Settings application, then choosing Network from the menu on the left. In the Wired section, click the gear icon to see the details. Here you'll find the IPv4 address, usually in form of four numbers separated by decimal points. We'll spend most of Module 3 discussing networking, so I won't go into too much detail here.

Once you have that IP address, switch to your Windows virtual machine, and open up the Firefox web browser. At the top in the address bar, simply input the IP address and press enter. If everything works correctly, you should be presented with the default Apache screen as seen here. If not, you'll need to do some debugging to figure out what is missing.

With that, you should now have all the information you need to finish the Ubuntu portion of Lab 1. If you have issues, please feel free to post in the course discussion forums or chat with me. Good luck!
