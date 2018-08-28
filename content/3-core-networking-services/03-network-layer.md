---
title: "3. Network Layer"
date: 2018-08-24T10:53:26-05:00
disableToc: true
disableMenu: true
---

{{< youtube  >}}

#### Resources

* **[Slides]({{< relref "03-network-layer-slides.md" >}})**
* [The TCP/IP Guide](http://www.tcpipguide.com/free/index.htm)
* [Classful Networks](https://en.wikipedia.org/wiki/Classful_network) on Wikipedia
* [Dot-Decimal Notation](https://en.wikipedia.org/wiki/Dot-decimal_notation) on Wikipedia
* [Classless Inter-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) on Wikipedia
* [IPv6](http://en.wikipedia.org/wiki/Ipv6) on Wikipedia
* [Reserved IP Addresses](https://en.wikipedia.org/wiki/Reserved_IP_addresses) on Wikipedia

#### Video Transcript

In this video, I'll discuss how the network layer of the 7-layer OSI model works.

The network layer is used to route packets from one host to another via a network. Typically, most modern networks today use the Internet Protocol or IP to perform this task, though there are other protocols available. In addition to computers, most routers also perform tasks at layer 3, since they need to be able to read and work with the address information contained in most network packets.

For most of the internet's history, the network layer used the Internet Protocol version 4, commonly known as IPv4. This slide gives the packet structure of IPv4, showing the information it adds to each packet that goes through that layer. The most important information is the source and destination IP address, giving the unique address on the network for the sender and intended recipient of this packet of information. Let's take a closer look at IP addresses, as they are a very important part of understanding how a computer network works.

For IPv4, an IP address consists of a 32-bit binary number, giving that host's unique identifier on the network. No two computers can share the same IP address on the same network. In most cases, the IP address is represented in Dot-Decimal notation.

Here's an example of that notation. Here, the binary number 10101100 is represented as the decimal number 172 in the first part of the IP address. Each block of 8 bits, or one byte, is represented by the corresponding decimal number, separated by a dot or period. This makes the address much easier to remember, almost like a phone number.

In fact, on the early days of the internet, that is exactly how it was set up. The early internet used a form of routing called "classful networking" to determine how IP addresses were divided. The type of network was determined by the first 4 bits of the IP address, much like an area code in modern phone numbers. There were several classes of networks, each of various sizes.

When an organization wanted to connect to the internet, they would register to receive a block of network addresses for their use. For a large network, such as IBM, they may receive an entire Class A network, whereas smaller organizations would receive a smaller Class B or Class C network. So, for a Class A network, the IP address would consist of the prefix 0, followed by 7 bits identifying the network. Then, the remaining 24 bits would identify the host on that network, usually assigned by the network owner. This helped standardize which parts of the IP address denoted the owner of the network, and which part denoted the unique computer on that network. For example, in this system, K-State would have the Class B network with the prefix 129.130.

You can even see some of this structure in this map of the IPv4 internet address space created by XKCD from several years ago. Many of the low numbered IP address blocks are assigned to a specific organization, representing the Class A networks those organizations had in the early days of the internet.

However, as the internet grew larger, this proved to be very inefficient. For example, many organizations did not use up all of their IP address space, leading to a large number of addresses that were unused yet unavailable for others to use. So, in the early 1990s, the internet switched to a new method of addressing, called Classless Inter-Domain Routing, or CIDR, sometimes pronounced as "cider." Instead of dividing the IPv4 address space into equal sized chunks, they introduced the concept of a subnet, allowing the address space to be divided in many more flexible ways.

Let's take a look at an example. Here, we are given the IP address 192.168.2.130, with the accompanying subnet mask of 255.255.255.0. To determine which part of the IP address is the network part, simply look at the bits of the IP address that correspond to the leading 1s in the subnet mask. If you are familiar with binary operations, you are simply performing the binary `and` operation on the IP and subnet to find the network part. Similarly, for the host part, look at the part of the IP address that corresponds to the 0s in the subnet mask. This would be equivalent to performing the binary `and` operation on the IP address and the inverse of the subnet mask.

Here's yet another example. Here, you can see that the subnet mask has changed, therefore the network and host portion of the IP address is different. In this way, organizations can choose how to divide up their allocated address space to better fit their needs.

To help make this a bit simpler, you can use a special form of notation called CIDR Notation to describe networks. In CIDR notation, the network is denoted by its base IP address, followed by a slash and the number of 1s in the subnet mask. So, for the first example on the previous slide, the CIDR notation of that network would be 192.168.2.0/24, since the network starts at IP address 192.168.2.0 and the subnet mask of 255.255.255.0 contains 24 leading 1s. Pretty simple, right?

With CIDR, an IP address can be subdivided many times at different levels. For example, several years ago the website freesoft.org had this IP address. Looking at the routing structure of the internet, you would find that the first part of that IP address was assigned to MCI, a large internet service provider. They then subdivided their network among a variety of organizations, one of those being Automation Research Systems, who received a smaller block of IP addresses from MCI. They further subdivided their own addresses, and eventually one of those addresses was used by freesoft.org.

The groups who control the internet, the Internet Engineering Task Force (IETF) and the Internet Assigned Numbers Authority (IANA), have also marked several IP address ranges as reserved for specific uses. This slide lists some of the more important ranges. First, they have reserved three major segments for local area networks, listed at the top of this slide. Many of you are probably familiar with the third network segment, starting with 192.168, as that is typically used by home routers. If you are using the K-State wireless network, you may notice that your IP address begins with a 10, which is part of the first segment listed here. There are also three other reserved segments for various uses. We'll discuss a couple of them in more detail later in this module.

However, since many local networks may be using the same IP addresses, we must make sure that those addresses are not used on the global internet itself. To accomplish this, most home routers today perform a service called Network Address Translation, or NAT. Anytime a computer on the internal network tries to make a connection with a computer outside, the NAT router will replace the source IP address in the packet with its own IP address, while keeping track of the original internal IP address. Then, when it receives a response, it will update the incoming packet's destination IP address with the original internal IP of the sender. This allows multiple computers to share the same external IP address on the internet. In addition, by default NAT routers will block any incoming packets that don't have a corresponding outgoing request, acting as a very powerful firewall for your internal network. If you have ever hosted a server on your home network, you are probably familiar with the practice of port-forwarding on your router, which adds and entry to your router's NAT table telling it where to send packets it receives.

For many years, IPv4 worked well on the internet. However, as internet access became more common, they ran into a problem. IPv4 only specified internet addresses which were 32-bits in length. That means that there are only about 4.2 billion unique IPv4 addresses available. With a world population over 7 billion, this very quickly became a limiting factor. So, as early as the 1990s, they began work on a new version of the protocol, called IPv6. IPv6 uses 128-bit IP addresses, allowing for 340 undecillion unique addresses. According to a calculation posted online, assuming that there was a planet with 7 billion people on it for each and every star in each and every galaxy in the known universe, you could assign each of those people 10 unique IPv6 addresses and still have enough to do it again for 10,000 more universes. [Source](https://skeptics.stackexchange.com/questions/22501/are-there-enough-ipv6-addresses-for-every-atom-on-the-surface-of-the-earth)

IPv6 uses a very similar packet structure to IPv4, with things simplified just a bit. Also, you'll note here that the source and destination addresses are 4 times as large, making room for the larger address space.

IPv6 addresses, therefore, are quite a bit different. They are represented digitally as 128-bit binary numbers, but typically we write them as 8 groups of 4 hexadecimal digits, sometimes referred to as a "hextet," separated by colons. Since IPv6 addresses are very long, we've adapted a couple of ways to simplify writing them.

For example, consider this IPv6 address. To simplify it, first you may omit any leading zeros in a block. Then, you can combine consecutive blocks of 0 together, replacing them with a double colon. However, you may only do that step once per address, as two instances of it could make the IP address ambiguous. Finally, we can remove all spaces to get the final address, shown in the last line.

IPv6 addresses use a variety of different methods to denote which part of the address is the network and host part. In essence, this is somewhat similar to the old classful routing of IPv4 addresses. Each prefix on an IPv6 address indicates a different type of address, and therefore a different parsing method. This slide gives a few of the most common prefixes you might see.

For this course, I won't go too deep into IPv6 routing, as most organizations still primarily use IPv4 internally. In addition, in many cases the network hardware automatically handles converting between IPv6 and IPv4 addresses, so you'll spend very little time configuring IPv6 unless you are working for an ISP or very large organization.

In the next video, we'll continue this discussion on the transport layer. 
