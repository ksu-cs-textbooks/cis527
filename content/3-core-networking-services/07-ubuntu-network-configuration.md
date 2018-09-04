---
title: "Ubuntu Network Configuration"
weight: 35
pre: "7. "
---

{{< youtube  >}}

#### Resources

* [How to Configure Static IP Address on Ubuntu 18.04 Bionic Beaver Linux](https://linuxconfig.org/how-to-configure-static-ip-address-on-ubuntu-18-04-bionic-beaver-linux) from LinuxConfig.org
* [How to Configure Static IP Address on Ubuntu 18.04](https://linoxide.com/linux-how-to/configure-static-ip-address-ubuntu/) from LinOxide
* [Network Configuration](https://help.ubuntu.com/lts/serverguide/network-configuration.html) from Ubuntu Server Guide.
* ['ip' Command Cheat Sheet (Command Line Reference)](https://www.thegeekdiary.com/ip-command-cheat-sheet-command-line-reference/) from The Geek Diary
* [ip Command Cheat Sheet](https://access.redhat.com/sites/default/files/attachments/rh_ip_command_cheatsheet_1214_jcs_print.pdf) from Red Hat
  - _Even though it is for Red Hat, most of these commands should also work in Ubuntu, and honestly, it is just a really handy cheat sheet to have!_
* [12 ip Command Examples for Linux Users](https://www.linuxtechi.com/ip-command-examples-for-linux-users/) from Linuxtechi
* [How to Use IPRoute2 Tools to Manage Network Configuration on a Linux VPS](https://www.digitalocean.com/community/tutorials/how-to-use-iproute2-tools-to-manage-network-configuration-on-a-linux-vps#how-to-configure-network-interfaces-and-addresses) from DigitalOcean
* [How to Use Traceroute and MTR to Diagnose Network Issues](https://www.digitalocean.com/community/tutorials/how-to-use-traceroute-and-mtr-to-diagnose-network-issues) from DigitalOcean
* [An Introduction to the ss Command](https://www.linux.com/learn/intro-to-linux/2017/7/introduction-ss-command) from The Linux Foundation
* [10 Examples of Linux ss Command to Monitor Network Connections](https://www.binarytides.com/linux-ss-command/) from BinaryTides

#### Video Transcript

Now, let's look at how to manage and configure a network connection in Ubuntu 18.04.

To begin, I'm working in the Ubuntu VM I created for Lab 2, with the Puppet Manifest files applied.

First, let's take a quick look at how our networking is configured in VMWare. This information is also covered in the video on Windows networking, but it is relevant here as well, since this will be very important as you complete Lab 3. To view the virtual networks in VMWare Workstation, click the **Edit** menu, then choose **Virtual Network Editor**. On VMWare Fusion, you can find this by going to the **VMWare Fusion** menu, selecting **Preferences**, then the **Network** option.

Here, we can see the virtual networks available on your system. Right now, there are two networks on my system, one "Host-only" network, and one "NAT" network. For this lab, we'll be working with the "NAT" network, so let's select it.

First, let's look at the network type, listed here. For this module, it is very important to confirm that the network type is set to "NAT" and not "Bridged." If you use a "Bridged" network for this lab, you could easily break the network that your host computer is connected to, and in the worst case earn yourself a visit from K-State IT staff as they try to diagnose the problem. So, make sure it is set correctly here!

We can also see lots of information about the network's settings. For example, we can see the subnet IP here, and the subnet mask here. By clicking on the **NAT Settings** button, I can also find the gateway IP. The gateway IP is the IP of the router, which tells your system where to direct outgoing internet traffic. You'll want to make a note of all three of those, as we'll need them later to set a static IP in Windows. You can also click the **DHCP Settings** button to view the settings for the DHCP server, including the range of IP addresses it uses, which can also be very helpful. If you want to change any of these settings, you can click the **Change Settings** button at the bottom. You'll need Administrator privileges to make any changes.

Next, let's confirm that our VM is using that virtual network. To do so, click the **VM** menu, then select **Settings**, then choose the **Network Adapter**. Make sure the network connection is set to "NAT" here as well.

Ok, now let's look at the network configuration in Ubuntu. In this video, I'll discuss how to view and update the network settings using the GUI. There are, of course, many ways to edit configuration files on the terminal to accomplish these tasks as well. However, I've found that the desktop version of Ubuntu works best if you stick with the GUI tools.

You can access the network settings by clicking the **Activities** button and searching for **Settings**, then selecting the **Network** option. As with Windows, you can right-click the networking icon in the notification area, then select the network connection you wish to change, and choosing the appropriate settings option in that menu.

Once in the **Settings** menu, click the **Gear** icon next to the connection you'd like to configure. The **Details** tab will show you the details of the current connection, including the IP address, MAC address, default gateway, and any DNS servers. On the **Identity** tab, you'll see that you can edit the name of the connection, as well as the MAC address.

To change the network settings, click the **IPv4** tab. Here, you can choose to input a manual IP address. If I select that option, I'll have to enter an IP address, subnet mask, and default gateway. For the IP address, I'll just make sure that it isn't in use on the network by picking one outside the DHCP range used by VMWare. The subnet mask and default gateway should be the same as the ones you found in the VMWare network settings earlier. Finally, we'll need to enter some DNS servers. Typically, you can just enter the same IP address as your default gateway, as most routers also can act as DNS resolvers as well. You can also use other DNS servers, such as those from OpenDNS or Google, as described in the Lab 3 assignment.

Once you have made your changes, click the green Apply button in the upper-right corner to apply your changes. If everything is successful, I should still be able to access the internet. Let's open a web browser, just to be sure.

Ubuntu includes a number of tools to help troubleshoot and diagnose issues with your network connection. Most of these are accessed via the command line. So, let's open a Terminal window. First, you can view available network devices using the `networkctl` command. You can also view their status using `networkctl status`.

If you've worked with Linux in the past, you're probably familiar with the `ifconfig` command. However, in recent years it has been replaced with the new `ip` command, and Ubuntu 18.04 is the first LTS version of Ubuntu that doesn't include `ifconfig` by default. So, we'll be using the newer commands in this course.

The first command to use is the `ip address show` command. This command will show you quite a bit of information about each network adapter on your system, including the IP address. You can also find the default gateway using `ip route show`. The new `ip` command has many powerful options that are too numerous to name here. I highly recommend reviewing some of the resources linked below the video to learn more about this powerful command.

In addition, Ubuntu includes a `ping` command, very similar to the one included in Windows. It uses the Internet Control Message Protocol, or ICMP, which allows it to send a simple "echo" request to the server. Most servers will respond to that request, allowing you to confirm that you are able to communicate with it properly across the internet. While that may seem like a very simple tool, it can actually be used in very powerful ways to diagnose a troublesome internet connection. On Ubuntu, note that by default the `ping` command will continuously send messages until you stop the command using `CTRL+C`. You can also specify the number of messages to send using the `-c <number>` option, such as `ping 192.168.0.1 -c 4` to send 4 messages to that IP address.

Similarly, the `mtr` command will use a series of ICMP "echo" messages to trace the route across the internet from your computer to any other system. This is similar to the `tracert` command on Windows, and, in fact, there is a similar `traceroute` command which can be installed on Ubuntu. However, it has been deprecated in favor of `mtr` in recent versions of Ubuntu. See the video on troubleshooting in this module for more information on how to troubleshoot connections using these tools.

Finally, Ubuntu also has a tool that can be used to examine TCP sockets. Previously, you would use the `netstat` command for this purpose, but it has been replaced by the new `ss` command, short for "socket statistics." For example, using just the `ss` command will get a list of all sockets, much like what TCPView will show on Windows. You can find just the listening TCP sockets by using `ss -lt`. As with the other commands, there are many different uses for this command. Consult the resources linked below this video for more information on how to use it.

With that information in hand, you should be able to complete Task 2 of this lab assignment, which is to set a static IP address on your Ubuntu VM acting as the server. If you run into any issues, please post in the course discussion forums to get help. Good luck!
