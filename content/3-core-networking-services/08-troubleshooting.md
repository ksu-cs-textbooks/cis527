---
title: "Troubleshooting"
weight: 40
pre: "8. "
---

{{< youtube  >}}

#### Resources

* [Network Hardware Troubleshooting Flowchart](https://www.fonerbooks.com/network.htm) from Foner Books
* [Basic Network Troubleshooting](https://www.computerhope.com/issues/ch000445.htm) from Computer Hope
* [7 Simple Steps to Diagnose a Network Problem](https://www.makeuseof.com/tag/7-simple-steps-diagnose-network-problem/) from MakeUseOf
* [Windows Network Troublehshooting Guide](https://www.makeuseof.com/tag/windows-network-troubleshooting-guide/) from MakeUseOf
* [The Art of Network Troubleshooting](https://www.computerworld.com/article/2545775/networking/the-art-of-network-troubleshooting.html) by Greg Schaffer on Computerworld


#### Video Transcript

When you are working with network connections, you'll inevitably run into issues. Understanding how to perform basic network troubleshooting is a very important skill for any system administrator to have, and it is one that you'll find yourself using time and time again. In this video, I'm going to briefly review some of the steps that you can take to diagnose and fix network issues.

As a quick side-note, many of the resources linked below this video still refer to older Linux commands such as `ifconfig` and `traceroute` instead of their newer counterparts. So, you may have to translate the commands a bit to get them to work on newer systems, but the process and theory itself should still apply.

In addition, many of these troubleshooting tools can be blocked by restrictive firewall rules. So, you'll need to be aware of your current firewall configurations and adjust as necessary. If possible, you could disable firewalls for testing, but that also could create a security concern. So, make sure you keep in mind the fact that firewalls can also be the root cause of many of these symptoms.

First, when faced with any unknown network issue, the very first step is to reboot any and all devices involved if possible. This includes your computer, routers, switches, modems, and any other networking devices along the path between your system and the intended destination. While this may seem drastic, in many cases it could be a simple fault in the hardware or networking software that a quick reboot will fix, while diagnosing and fixing the error without a reboot may be nearly impossible. Of course, in an enterprise setting, you probably don't want to reboot your entire network infrastructure each time you have an issue, so you'll have to examine the tradeoffs before doing so. On a home network, however, rebooting the computer and router is a pretty negligible cost.

Next, I recommend determining how far across the network you can reach. In effect, this helps you pinpoint the exact root cause of the network issue, and it will tell you where to focus your efforts. This process can be performed on almost any operating system, as long as it has the `ping` command available, as well as a command to display the current IP address.

First, you'll need to determine if your computer is able to connect to itself. You can do so by using the `ping` command to send requests to the loopback interface on your system. To do so, use these two commands:

```bash
ping 127.0.0.1
ping localhost
```

The first command pings the IP address of the loopback adapter, ensuring that the networking drivers in the operating system are working properly. If that command returns an error, or is not able to connect to your system, it most likely means your networking hardware or drivers on the local system are failing and need to be fixed. The second command pings the same address, but using the commonly available DNS name `localhost`. If that command fails, but the first one succeeds, it could mean that the DNS resolver or `hosts` file on your system is corrupt. If so, that's where you'll want to focus your efforts.

If you are able to successfully ping yourself, the next step is to determine if you have a valid IP address. You can use either the `ipconfig` command on Windows or the `ip` commands on Linux to find your current IP address. Then, use the `ping` command to make sure you can send and receive messages via that IP address. If that step fails, you may want to release and renew your IP address if you are using DHCP, or verifying that you have the correct IP settings if you are using a static IP address. To release and renew your IP address, use the following commands on Windows:

```powershell
ipconfig /release
ipconfig /renew
```
On Linux, it is a little less straightforward, but the best way to accomplish the same task is by using these commands:

```bash
sudo dhclient -r
sudo dhclient
```

If you are able to get a valid IP address using these steps, you can continue on to see if you are able to access the rest of the network. If not, you may need to check your network router settings or static IP address settings to make sure they are correct.

Next, you'll want to ping the default gateway address as configured in your system. Generally, that should be the address of your router on your network. You can find that address using the `ipconfig` and `ip` commands as described above. Use the `ping` command to try and reach that address. If it works, that means you are able to successfully contact your router. If not, it could be an issue with the network cables between you and your router, or a misconfiguration of either your router or static IP address. In either case, this is sometimes the most frustrating case to deal with, as you've ensured that your computer is working, but it cannot reach the core of your local network. I recommend looking at the [Network Hardware Troubleshooting Flowchart](https://www.fonerbooks.com/network.htm) from Foner Books to try and work your way through this problem.

If you are able to connect with your default gateway, the next step is to see if you can reach your intended destination. If it is another computer on your network or another network, try to ping it's IP address. If that connection fails, most likely the problem is somewhere between your router and that computer. In that case, you'll want to try this troubleshooting procedure again from that computer and see if you can pinpoint the problem.

If you are trying to reach a website on the internet, there are a couple more steps to perform here. First, if you know the public IP address and default gateway address your internet service provider, or ISP, is providing to you, you can try to ping those addresses. If they do not work, most likely the problem is with your network modem or your local ISP. In that case, you'll want to get in touch with them to try and resolve the issue.

Next, you should try to ping a server on the internet by IP address. I usually recommend either the OpenDNS servers, which are `208.67.222.222` and `208.67.220.220`, or the Google DNS servers, which are `8.8.8.8` and `8.8.4.4`. If you can reach those servers, your connection to the internet is definitely working. If not, the issue is also most likely with your ISP, and you'll need to contact them to resolve the problem.

Finally, you should try to ping a few web addresses by the DNS names. I usually recommend using an address that is guaranteed to be available, but one that won't be cached on the system. I hate to say it, but using search engines other than Google, such as www.bing.com or www.yahoo.com, are all great choices for this step. When you do so, you could receive a message that it is unable to resolve that DNS name into an IP address. If that is the case, you should check your DNS settings. If nothing else, you can always replace them with settings for OpenDNS or Google DNS and test with those addresses.

If you are able to resolve the IP address but are unable to reach them, then you could have a firewall issue of some kind. It is very rare that you are able to ping servers by IP address but not via the DNS names, so a firewall is the most likely culprit here.

Of course, if you are able to reach those sites correctly using `ping`, then the last step is to open a web browser and try to load one of those webpages. If that fails, then you'll need to examine either the browser software itself or the firewall. The firewall could be blocking HTTP connections, or the browser could be corrupted and need reinstalled. In either case, it is most likely a software issue at that point.

This is just a brief overview of some of the steps you could take to diagnose a network issue. To be honest, I could probably teach an entire course just on this one subject, since there are that many different things that could go wrong in a modern computer network. However, this should give you a set of universal tools you can use to help at least pinpoint the location of the error and narrow your search to a specific device or configuration for the source of the issue. Of course, as a last resort you can always search the internet for additional troubleshooting steps or advice, but remember that sometimes you aren't even able to do that when your internet isn't working. So, it helps to have a basic understanding of network troubleshooting and familiarity with a few quick tools to help you out.
