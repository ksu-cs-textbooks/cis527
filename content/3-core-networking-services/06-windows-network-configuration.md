---
title: "6. Windows Network Configuration"
date: 2018-08-24T10:53:26-05:00
---

{{< youtube  >}}

#### Resources

* [How to Assign a Static IP Address in Windows 7, 8, 10, XP, or Vista](https://www.howtogeek.com/howto/19249/how-to-assign-a-static-ip-address-in-xp-vista-or-windows-7/) from How-To Geek
* [How to Set a Static IP Address on Windows 10](https://pureinfotech.com/set-static-ip-address-windows-10/) from Pureinfotech
* [4 Common Windows Network Utilities Explained](https://www.maketecheasier.com/common-windows-network-utilities-explained/) from Make Tech Easier
* [TCPView](https://docs.microsoft.com/en-us/sysinternals/downloads/tcpview) from Windows Sysinternals

#### Video Transcript

Now, let's look at how to manage and configure a network connection in Windows 10.

To begin, I'm working in the Windows 10 VM I created for Lab 2, with the Puppet Manifest files applied.

First, let's take a quick look at how our networking is configured in VMWare. This will be very important as you complete Lab 3. To view the virtual networks in VMWare Workstation, click the **Edit** menu, then choose **Virtual Network Editor**. On VMWare Fusion, you can find this by going to the **VMWare Fusion** menu, selecting **Preferences**, then the **Network** option.

Here, we can see the virtual networks available on your system. Right now, there are two networks on my system, one "Host-only" network, and one "NAT" network. For this lab, we'll be working with the "NAT" network, so let's select it.

First, let's look at the network type, listed here. For this module, it is very important to confirm that the network type is set to "NAT" and not "Bridged." If you use a "Bridged" network for this lab, you could easily break the network that your host computer is connected to, and in the worst case earn yourself a visit from K-State IT staff as they try to diagnose the problem. So, make sure it is set correctly here!

We can also see lots of information about the network's settings. For example, we can see the subnet IP here, and the subnet mask here. By clicking on the **NAT Settings** button, I can also find the gateway IP. The gateway IP is the IP of the router, which tells your system where to direct outgoing internet traffic. You'll want to make a note of all three of those, as we'll need them later to set a static IP in Windows. You can also click the **DHCP Settings** button to view the settings for the DHCP server, including the range of IP addresses it uses, which can also be very helpful. If you want to change any of these settings, you can click the **Change Settings** button at the bottom. You'll need Administrator privileges to make any changes.

Next, let's confirm that our VM is using that virtual network. To do so, click the **VM** menu, then select **Settings**, then choose the **Network Adapter**. Make sure the network connection is set to "NAT" here as well.

Ok, now let's look at the network configuration in Windows 10. First, you can see information about the available network adapters in the Device Manager. You can access that by right-clicking on the **Start** button and choosing **Device Manager** from the list. On that window, expand the section for **Network Adapters**. Here, you'll see that this VM has a single network adapter, as well as a couple of Bluetooth devices available.

Next, let's look at the network settings for our network adapter. You can find these by right-clicking the **Start** button once again, and choosing **Network Connections**, or by right-clicking the **Network** icon in the notification area and selecting **Open Network & Internet Settings**. This will bring you to the **Network Status** window in the Settings app. While you can find quite a bit of information about your network settings here, I've found it is much easier to click the option below for **Change adapter options** to get to the classic **Network Connections** menu on the Control Panel.

Here, I can see all of the available network adapters on my system, as well as a bit of information about each one. Let's right-click on the Ethernet0 adapter, and select **Status**. This window will show the current connection status, as well as some basic statistics. You can click the **Details** button to view even more information, such as your IP address, MAC address, and more.

If you'd like to set a static IP address for this system, you'll need to click the **Properties** button at the bottom, then select the **Internet Protocol Version 4 (TCP/IPv4)** option, and finally **Properties** below that. On this window, you can set a static IP address for your system. To do so, I'll have to enter an IP address, subnet mask, and default gateway. For the IP address, I'll just make sure that it isn't in use on the network by picking one outside the DHCP range used by VMWare. The subnet mask and default gateway should be the same as the ones you found in the VMWare network settings earlier. Finally, we'll need to enter some DNS servers. Typically, you can just enter the same IP address as your default gateway, as most routers also can act as DNS resolvers as well. You can also use other DNS servers, such as those from OpenDNS or Google, as described in the Lab 3 assignment. Finally, I'll click OK to save and apply those settings. If everything is successful, I should still be able to access the internet. Let's open a web browser, just to be sure. For this lab assignment, you won't be setting a static IP on Windows 10, but you will use this process in the next module when you configure your first Windows server. The process is very similar.

Windows includes a number of tools to help troubleshoot and diagnose issues with your network connection. First off, the network troubleshooter available in the **Network & Internet Settings** menu is pretty good, and can help you figure out many simple issues with your network connection.

Beyond that, there are a few command-line tools that you should be familiar with on Windows. So, let's open a PowerShell window. The first command to use is `ipconfig`. This tool has been available in Windows since the earliest versions, and it can give you quite a bit of information about your network connection. Running it without any additional options will give you your IP address, subnet mask, default gateway, and other basic information for each of your network adapters.

You can also run `ipconfig /all` to see all the available information about all network adapters on your system. It gives quite a bit more information, including your MAC address and DHCP lease information.

That command also allows you to manage your DHCP client. For example, you can use `ipconfig /release` to release all DHCP addresses, then `ipconfig /renew` to request a new DHCP address. This is very handy if you have recently reset or reconfigured your network router, as you can tell Windows to just request a new IP address without having to reboot the system.

It can also help manage your DNS cache. Windows maintains a cache of all DNS requests and the responses you receive, so that multiple requests for the same DNS name can be quickly resolved without needing to query again. You can use `ipconfig /displaydns` to view the cached DNS entries, and `ipconfig /flushdns` to clear the cache. This is very handy when you are trying to diagnose issues with DNS on your system. Of course, DNS caching could create a privacy concern, as the DNS cache will contain information about all websites you've visited on this system. In fact, some anti-cheat programs for online video games have been found to check the Windows DNS cache, looking for entries from programs known to interfere with their games.

Finally, Windows includes a couple of really handy troubleshooting tools. First, you can use the `ping` command to send a simple message to any server on the internet. It uses the Internet Control Message Protocol, or ICMP, which allows it to send a simple "echo" request to the server. Most servers will respond to that request, allowing you to confirm that you are able to communicate with it properly across the internet. While that may seem like a very simple tool, it can actually be used in very powerful ways to diagnose a troublesome internet connection. Similarly, the `tracert` command will use a series of ICMP "echo" messages to trace the route across the internet from your computer to any other system. See the video on troubleshooting in this module for more information on how to troubleshoot connections using these tools.

The Windows Sysinternals suite of tools also includes one helpful tool, called **TCPView**, which allows you to view all of the active TCP connections on your system. This will show all open ports as well as any established connections. As you are working with networked programs, you can use TCPView to get a good idea of what connections are happening on your system. It can also help you diagnose some problems with programs and your firewall configuration. You can also use the `netstat` command in PowerShell to find similar information, but I prefer this graphical view.

That's all for configuring Windows networking. Stay tuned for information about configuring networking in Ubuntu!
