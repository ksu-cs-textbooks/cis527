---
title: "4. Transport Layer"
date: 2018-08-24T10:53:26-05:00
---

{{< youtube  >}}

#### Resources

* **[Slides]({{< relref "/3-core-networking-services/04-transport-layer-slides.md" >}})**
* [The TCP/IP Guide](http://www.tcpipguide.com/free/index.htm)
* [Transmission Control Protocol](https://en.wikipedia.org/wiki/Transmission_Control_Protocol) on Wikipedia
* [User Datagram Protocol](https://en.wikipedia.org/wiki/User_Datagram_Protocol) on Wikipedia
* [List of TCP and UDP Port Numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers) on Wikipedia

#### Video Transcript

Now, let's take a look at layer 4 of the OSI model - the transport layer.

The transport layer is responsible for facilitating host-to-host communication between applications on two different hosts. Depending on the protocol used, it may also offer services such as reliability, flow control, sustained connections, and more. When writing a networked application, your application typically interfaces with the transport layer, creating a particular type of network socket and providing the details for creating the connection. On most computer systems today, we use either the TCP or UDP protocol at this layer, though many others exist for various uses.

First, let's look at the Transmission Control Protocol, or TCP. It was developed in the 1980s, and is really the protocol responsible for unifying the various worldwide networks into the internet we know today. TCP is a stateful protocol, meaning that it is able to maintain information about the connection between packets sent and received. It also provides many services to make it a reliable connection, from acknowledging received packets, resending missed packets, and rearranging packets received out of order, so the application gets the data in the order it was intended. Because of this, we refer to TCP as a connection-oriented protocol, since it creates a sustained connection between two applications running on two hosts on the network.

Here is a simplified version of the state diagram for TCP, showing the process for establishing and closing a connection. While we won't focus on this process in this course, you'll see packets for some of these states a bit later when we use Wireshark to collect network packets.

Since TCP is a stateful protocol, it includes several pieces of information in its packet structure. The two most notable parts are the sequence and acknowledgement fields, which allow TCP to reorganize packets into the correct order, resend missing packets, and acknowledge packets that have been successfully received. In addition, you'll notice that it lists a source and destination port, which we'll cover shortly.

The other most commonly used transport layer protocol is the User Datagram Protocol, or UDP. Unlike TCP, UDP is a stateless, unreliable protocol. Basically, when you send a packet using UDP, you are given no guarantees that it will arrive, or no acknowledgement when it does. In addition, each packet sent via UDP is independent, so there is no sustained connection between two hosts. While that may seem to make UDP completely useless, it actually has several unique uses. For example, the domain name system or DNS uses UDP, since each DNS lookup is essentially a single packet request and response. If a request is sent and no response is received quickly enough, it can simply resend another request, without the extra overhead of maintaining any state for the previous connection. Similarly, UDP is also helpful for streaming media. A single lost packet in a video stream is not going to cause much of an issue, and by the time it could be resent, it is already too old to be of use. So, by using UDP, the stream can have a much lower overhead, and as long as enough packets are received, the stream can be displayed.

Since UDP is stateless, the packet structure is also much simpler. It really just includes a source and destination port, as well as a length and checksum field to help make sure the packet itself is correct.

So, to quickly compare TCP and UDP, TCP is great for long, reliable connections between two hosts, whereas UDP is great for short bursts of data which could be lost in transit without affecting the application itself.

One great way to remember these is through the two worst jokes in the history of Computer Science.

> Want to hear a TCP joke? Well, I could tell it to you, but I'd have to keep repeating it until I was sure you got it.  

> Want to hear a UDP joke? Well, I could tell it to you, but I'd never be sure if you got it or not.

See the difference?

Both TCP and UDP, as well as many other transport layer protocols, use ports to determine which packets are destined for each application. A port is simply a virtual connection point on a host, usually managed by the networking stack inside the operating system. Each port is denoted by a 16-bit number, and typically each port can only be used by one application at a time. You can think of the ports like the name on the envelope from our previous example. Since multiple people could share the same address, you have to look at the name on the envelope to determine which person should open it. Similarly, since many programs can be running on the same computer and share the same IP, you must look at the port to figure out which program should receive the packet.

There are several ports that are considered "well known" ports, meaning that they have a specific use defined. While there is no rule that says you have to adhere to these ports, and in some cases it is advantageous to ignore them, these "well known" ports are what allows us to communicate easily over the internet. When an application establishes an outgoing connection, it will be assigned a high-numbered "ephemeral" port to use as the source port, whereas the destination port is typically a "well known" port for the application or service it wishes to communicate with. In that way, there won't be any conflicts between a web browser and a web server operating on the same host. If they both tried to use port 80, it would be a problem!

When ports are written with IP addresses, they are typically added at the end following a colon. So, in this example, we are referencing port 1234 on the computer with IP address 192.168.0.1.

There are over 1000 well known ports that have common usage. Here are just a few of them, along with the associated application or protocol. We'll look more closely at several of these protocols later in this module.

 So, to summarize the OSI 7-layer network model, here's the overall view of the postal service analogy we've been using. At layers 5-7, you would write a letter to send to someone. At layer 4, the transport layer, you'd add the name of the person you'd like to send it to, as well as your own name. Then, at layer 3, the network layer would add the to and from mailing address. Layer 2 is the post office, which would take your envelope and add it to a box. Then, at the physical layer, a truck would transport the box containing your letter along its path. At several stops, the letter may be inspected and placed in different boxes, similar to how a router would move packets between networks. Finally, at the receiving end, each layer is peeled back, until the final letter is available to the intended recipient.

 In networking terms, the application creates a packet at layers 5 - 7. Then, the transport layer adds the port, and the network layer adds the IP addresses to the packet. Then, the data link layer puts the packet into one or more frames, and the physical layer transmits those frames between nodes on the network. At some points, the router will look at the addresses from the third layer to help with routing the packet along its path. Finally, once it is received at the intended recipient, the layers can be removed until the packet is presented to the application.

 I hope these videos help you better understand how the OSI 7-layer network model works. Next, we'll discuss how to use these concepts to connect your systems to a network, as well as how to troubleshoot things when those connections don't work.
