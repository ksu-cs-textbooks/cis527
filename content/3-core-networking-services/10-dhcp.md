---
title: "DHCP"
weight: 50
pre: "10. "
---

{{< youtube BytkMTK84jM >}}

#### Resources

* **[Slides]({{% relref "/3-core-networking-services/10-dhcp-slides.md"  %}})**
* [Dynamic Host Configuration Protocol (DHCP)](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol) on Wikipedia
* [Bootstrap Protocol (BOOTP)](https://en.wikipedia.org/wiki/Bootstrap_Protocol) on Wikipedia
* [What is DHCP? (Dynamic Host Configuration Protocol)](https://www.lifewire.com/what-is-dhcp-2625848) from Lifewire
* [ISC DHCP](https://www.isc.org/downloads/dhcp/) Open Source Software for DHCP Servers
* [Dynamic Host Configuration Protocol](https://tools.ietf.org/html/rfc2131) (RFC 2131) Standard from IETF
* [Link-Local Address](https://en.wikipedia.org/wiki/Link-local_address) on Wikipedia

#### Video Transcript

The Dynamic Host Configuration Protocol, or DHCP, is a core part of operating any network today. This video will introduce DHCP and demonstrate how it works. In your lab assignment, you'll be setting up and configuring your own DHCP server, so this information will be very helpful in completing that task.

As a quick note, much of the information in this lecture is adapted from information provided by Seth Galitzer, our system administrator here in K-State CS. He created the original slides as part of a guest lecture in this course when it was offered on campus, and was gracious enough to share this information for future versions of the course.

First, let's review a bit of internet history. Prior to the 1980s, there were many networks that existed across the world, but they were not interconnected. In 1982, the TCP and IP protocols were developed, with the aim of unifying all of those networks into a grand interconnected network, or "internet." At the time, there were only a few hundred computers worldwide which would be part of this network, so manual configuration wasn't too bad. As there were more and more computers on the internet, they realized that it would be helpful to have a way to automatically configure new systems. So, in 1985, the Bootstrap Protocol, or BOOTP, was developed in order to provide some automation. However, BOOTP was very limited, and only could perform some functions. As the internet was growing by leaps and bounds at this point, they decided a new solution was needed. So, in 1989, they formed the DHC working group to build a better way. In 1993, their initial specification for DHCP was released, and in 1996 the first working server was available. A year later, in 1997, they finalized the protocol into the standard it is today.

There were some major reasons why DHCP was needed. As discussed, the internet, as well as many corporate networks, were getting larger and larger, and manual configuration of those networks was simply too difficult to manage. In addition, with the introduction of laptops and mobile devices, computers needed to be able to seamlessly move from network to network without needing additional configuration. So, they really needed a method to automatically configure network settings on a computer when it initially connected to a network. Hence, the creation of DHCP.

Beyond that, there are many features built in to DHCP to make it a very powerful system. First, it includes the concept of "leasing" an IP address. When a system first connects to the network, it is given an IP address and a length of time it may keep that IP address. Once that time is up, it must renew its lease on that IP, or the system may assign that IP to a new system. In this way, as systems come and go, the DHCP server can reuse IP addresses once the leases have expired. In addition to IP addresses, modern DHCP servers can also send additional information about the network, such as DNS servers, SMTP servers, and more. Using DHCP, modern computers can be much more portable, allowing them to seamlessly connect to any network providing a DHCP server. Finally, even though DHCP is very powerful, there are many instances where a static IP address is preferred, such as for servers and printers. Thankfully, DHCP is fully compatible with static IP addresses on the same network. All that is required is a bit of configuration to mark which sections of the network should be automatically configured and which shouldn't. In addition, many DHCP servers can be configured to always give the same IP address to a particular host, providing even more flexibility.

Let's dig a bit deeper in to the DHCP protocol itself to see how it works. In essence, DHCP is a 4-step handshake that happens when any new computer connects to a network. In the first step, the computer sends out a special "discover" message to every system on the network, asking for help to connect. That message is sent to the destination IP address 255.255.255.255, which is a special broadcast address telling the network to send that packet to every computer on the network. This allows the computer to communicate, even if it doesn't have the proper network settings yet. In the second step, a DHCP server will receive that "discover" message, and send back an "offer" message containing an IP address and additional settings the computer could use. Once the computer receives that message, it will then broadcast a "request" message, which requests a specific IP address. It could be one it was using previously if it is renewing a lease, otherwise it will be one from the "offer" message it received. When the DHCP server receives that "request" message, if that IP address is still available, it will respond with an "acknowledge" message confirming the address, or it will respond with an error to the computer, which starts the process over again. Once the computer receives an "acknowledge" message, it can then configure its network settings using the information it has received, and it is good to go.

So, in short, it goes something like this:

1. Client: "Hi, I'm new!"
1. Server: "Welcome! Here's some settings you could use."
1. Client: "Cool! Can I use these settings?"
1. Server" "Sure can! You are all set."

DHCP also works with multiple servers. Since each server will receive the "discover" message, it will respond with its own "offer" message. The computer can then choose which "offer" to respond to, and the servers will only respond with an "acknowledge" message if it was the original sender of the offer. In that way, you can have multiple DHCP servers available on the network, providing additional redundancy and capacity.

If a computer fails to get an IP address from DHCP, it can automatically configure an IP address using the Automatic Private IP Address (APIPA) configuration protocol. In essence, it will assign an IP address in the link-local subnet, that allows it to work on the network without conflicting with anything else. Both IPv4 and IPv6 have set aside a block addresses for this use.

Seth was also gracious enough to provide some sample DHCP configuration files. These were used on CS systems when the department was located in Nichols Hall years ago. Here at the top, you can see the configuration settings for the DHCP lease time. By default, each lease is good for 10 minutes, but clients can request a lease as long as 2 hours (120 minutes, or 7200 seconds). Below that, we can see some default settings for the network, giving the domain name, DNS servers, subnet mask, broadcast addresses, and more for this network.

Here we can see an example for a fixed-address configuration. Whenever a computer contacts this server using that MAC address, it will be assigned the IP address listed below. This is very handy when you have laptops that may come and go on the network. In this way, they are always configured to use DHCP so that the user can use them elsewhere without any problems, but when they are connected to this network they are effectively given a static IP address. Finally, below that we can see a configuration for a simple pool of IP addresses available for automatic configuration.

Of course, this is not a complete configuration file, nor will any of these settings work for your lab assignment. So, you'll need to read the appropriate documentation as well as discover your own network's settings in order to configure your DHCP server.

Let's look at a quick example of how this would look in practice. Here I have configured an Ubuntu VM as directed in Lab 3 to act as a DHCP and DNS server. I also have a second Ubuntu VM acting as our client. Finally, I have disabled the DHCP server in VMware on this network segment.

First, on my server, I'm going to start Wireshark so we can capture these packets. I'll also add a filter for `bootp` to make sure we only see the DHCP server packets. Since BOOTP and DHCP are compatible protocols, this is the way that Wireshark sees the packets.

Next, I'm going to boot up the client, which will cause it to request an IP address as it boots. Once it has booted and I've logged in, I'm also going to release my IP address:

```bash
sudo dhclient -r -v
```

This should show that it sent a `DHCPRELEASE` packet to my DHCP server. Then, after waiting a few seconds, we can request a new IP address:

```bash
sudo dhclient -v
```

Examining the output, you'll see that we send a `DHCPDISCOVER` message, then we receive a `DHCPOFFER` from the server. We can then request an IP using a `DHCPREQUEST` message, and finally we'll receive a `DHCPACK` message back from the server acknowledging that request. Here, you'll notice that we send the `DHCPREQUEST` before we even receive the `DHCPOFFER`. Since we had an IP previously, we can just go ahead and request it again and see if it works. If so, we'll be on the network a little bit faster, but if not, we can just respond to the `DHCPOFFER` we receive and continue the original handshake.

Going back to the server, we can clearly see those four packets, as well as the earlier `DHCPRELEASE` packet. By examining any of those packets, we can see the different bits of information sent from the server to the client and vice-versa.

In addition, by default the DHCP server will log information to the system log, so we can find information about these packets by searching through that log file:

```bash
cat /var/log/syslog | grep dhcp
```

When troubleshooting a DHCP server, it is very helpful to review any error messages present in the system log.

With that information, you should be ready to configure your own DHCP server. As always, if you have any questions or run into issues, please post in the course discussion forums on Canvas. This process can definitely be frustrating the first time you do it, since there is so much new information to read and understand. Don't be afraid to ask for help if you get stuck!
