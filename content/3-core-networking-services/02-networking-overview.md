---
title: "2. Networking Overview"
date: 2018-08-24T10:53:26-05:00
disableToc: true
disableMenu: true
---

{{< youtube  >}}

#### Resources

* **[Slides]({{< relref "02-networking-overview-slides.md" >}})**
* [The TCP/IP Guide](http://www.tcpipguide.com/free/index.htm)
* [Packet Switching](https://en.wikipedia.org/wiki/Packet_switching) on Wikipedia
* [Computer Network](https://en.wikipedia.org/wiki/Computer_network) on Wikipedia
* [Spanning Tree Protocol](https://en.wikipedia.org/wiki/Spanning_Tree_Protocol) on Wikipedia
* [Basics of Computer Networking](https://www.geeksforgeeks.org/basics-computer-networking/) from GeeksforGeeks

#### Video Transcript

Before we start working with networking on our virtual machines, let's take a few minutes to discuss some fundamental concepts in computer networking.

For most people, a computer network represents a single entity connecting their personal computer to "The Internet," and not much thought is given to how it works. In fact, many users believe that there is a direct line from their computer directly to the computer they are talking with. While that view isn't incorrect, it is definitely incomplete.

A computer network more closely resembles this diagram. Here we have three computers, connected by six different network devices. The devices themselves are also interconnected, giving this network a high level of redundancy. To get from Computer A to Computer B, there are several possible paths that could be taken, such as this one. If, at any time, one of those network links goes down, the network can use a different path to try and reach the desired endpoint.

This is all due to the fact that computer networks use a technology called "packet switching." Instead of each computer talking directly with one another, as you do when you make a long-distance phone call, the messages sent between two computers can be broken into packets, and then distributed across the network. Each packet is able to make its way from the sender to the receiver, where they are reassembled into the correct message. A great analogy to this process is sending a postcard through the mail. The postal service uses the address on the postcard to get it from you to its destination, but the path taken may change each time. At each stop along the way, the post office determines what the best next step would be, hopefully getting your postcard closer to the correct destination each time. This allows your postcard to get where it needs to go, without anyone ever trying to determine the entire route beforehand.

When we scale this up to the size of the internet, visualized here, it is really easy to see why this is important. By using packet switching, a message can get from one end of the internet to the other without needing to take the time to figure out the entire path beforehand. It can simply move from one router to another, each time taking the most logical step toward its destination.

Modern computer networks use a theoretical model called the Open Systems Interconnection (or OSI) model, commonly referred to as the OSI 7-Layer model, to determine how each part of the network functions. For system administrators, this model is very helpful as it allows us to understand what different parts of the network should be doing, without worrying too much about the underlying technologies making it happen. In this module, we'll look at each layer of this model in detail.

When an application wants to communicate across a network, it generates a data packet starting at layer 7, the application layer, on the computer it is sending from. Then, the packet moves downward through the layers, with each layer adding a bit of information to the packet. Once it reaches the bottom layer, it will be transmitted to the first hop on the network, usually your home router. The router will then examine the packet to determine where it needs to go. It can do so by peeling back the layers a bit, usually to layer 3, the network layer, which contains the IP address of the destination. Then, it will send the packet on its way to the next hop. Once it is received by the destination computer, it will move the packet back up the layers, with each one peeling off its little bit of information. Finally, the packet will be received by the destination application.

As we discussed, each layer adds a bit of information to the packet as it moves down from the application toward the physical layer. This is called encapsulation. To help understand this, we can return to the postal service analogy from earlier. Let's say you'd like to send someone a letter. You can write the letter to represent the packet of data you'd like to send, then place it in a fancy envelope with the name of the recipient on it. Then, you'll place that envelope in a mailing envelope, and put the mailing address of the recipient on the outside. This is effectively encapsulating your letter, with each layer adding information about where it is destined. Then, the postal service might add a barcode to your letter, and place it in a large box with other letters headed to the same destination, further encapsulating it. Once it reaches the destination, each layer will be removed, slowly revealing the letter inside.

In this video, we'll discuss the bottom two layers of the model, the physical and data link layers. Later videos will discuss the other layers in much more detail.

First, the physical layer. This layer represents the individual bytes being sent across the network, one bit at a time. Typically this is handled directly in hardware, usually by your network interface card or NIC. There are many different ways this can be done, and each type of network has a different way of doing it. For this class, we won't be concerned with that level of detail. If you hear things such as "100BASE-T" or "1000BASE-T" or "gigabit," those terms are typically referring to the physical layer.

The next layer up is the data link layer. At this layer, data consists of a frame, which is a standard sized chunk of data to be sent from one computer to another. A packet may fit inside of a frame, or a packet may be further divided into multiple frames, depending on the system and size of the packet. Some common technologies used at this layer are Ethernet, and the variety of 802.11 wireless protocols, among others.

The major networking item handled by the data link layer is routing. Routing is how each node in the network determines the best path to get from one point to another on the network. It is also very important in allowing the network to have redundant connections while preventing loops across those connections. To determine how to route a packet, most networks use some variant of a spanning tree algorithm to build the network map. Let's see how that works.

To start, here is a simple network. There are 6 network segments, labeled a through f. There are also 7 network bridges connecting those segments, numbered with their ID on the network. To begin, the network bridge with the lowest ID is selected as the root bridge. Next, each bridge determines the least-cost path from itself to the root bridge. The port on that bridge in the direction of the root bridge is labelled as the root port, or RP in this diagram. Then, the shortest path from each network segment toward the root bridge is labelled as the designated port, or DP. Finally, any ports on a bridge not labelled as a root port or designated port are blocked, labelled BP on this diagram.

Now, to get a message from network segment f to the root bridge, it can send a message toward its designated port, on bridge 4. Then, bridge 4 will send the packet out of its root port into segment c, which will pass it along its designated port on bridge 24. The process continues until the packet reaches the root bridge. In this way, any two network segments are able to find a path to the root bridge, which will allow them to communicate.

If, at any time a link is broken, the spanning tree algorithm can be run again to relabel the ports. So, in this instance, segment f would now send a message toward bridge 5, since the link between segment c and bridge 24 is broken.

Finally, the other important concept at layer 2 is the use of virtual local area networks, or VLANs. A VLAN is simply a partition of a network at layer 2, isolating each network. In essence, what you are doing is marking certain ports of a router as part of one network or another, and telling the router to treat them as separate networks. In this way, you can simplify your network design by having systems grouped by function, and not by location.

Here's a great example. In this instance, we have a building with three floors. Traditionally, each floor would consist of its own network segment, since typically there would be one router per floor. Using VLANs, we can rearrange the network to allow all computers in the engineering department to be on the same network segment, even though they are spread across multiple floors of the building.

In the real world, VLANs are used extensively here at K-State. For example, all of the wireless access points are on the same VLAN, even though they are spread across campus. The same goes for any credit card terminals, since they must be protected from malicious users attempting to listen for credit card numbers on the network.

Most enterprise-level network routers are able to create VLANs, but many home routers do not support that feature. Since we won't be working with very large networks in this course, we won't work with VLANs directly. However, they are very important to understand, since most enterprises make use of them.

In the following videos, we'll discuss the next layers of the OSI model in more detail.
