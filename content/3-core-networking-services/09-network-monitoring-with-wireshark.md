---
title: "Network Monitoring with Wireshark"
weight: 45
pre: "9. "
---

{{< youtube  >}}

#### Resources

* **[Slides]({{< relref "/3-core-networking-services/09-network-monitoring-with-wireshark-slides.md" >}})**
* [Wireshark Documentation](https://www.wireshark.org/docs/)
* [How to User Wireshark to Capture, Filter, and Inspect Packets](https://www.howtogeek.com/104278/how-to-use-wireshark-to-capture-filter-and-inspect-packets/) from How-To Geek

#### Video Transcript

Many times when you are working with networks as a system administrator, it is helpful to be able to see the actual traffic being sent across the network. Thankfully, there are many tools available to help you do just that. In this video, I'll introduce one of those tools, named Wireshark.

Wireshark originally began as Ethereal, a network monitoring program developed in 1998 by Gerald Combs. In 2006, the name was changed to Wireshark to avoid copyright issues, and has been under constant development ever since. It is completely open source under the GNU General Public License, or GPL. Wireshark can be used to capture and inspect individual packets of network traffic, and it natively understands and decodes several hundred different protocols, giving you a very handy way to inspect not only the type of traffic on your network, but the contents of those packets.

Before we continue, there is one important warning I must share with you. Using Wireshark on a network allows you to potentially intercept and decode any unencrypted packets on the network, regardless of whether they are sent or received by your computer. This is a violation of K-State's IT policies, and therefore you should never use Wireshark while directly connected to K-State's network. As long as you are only using Wireshark within your VM network, and you've confirmed that your VM network is not set to "bridged" mode, you should be fine. So, make sure you are very careful when using this tool.

First, we'll need to install Wireshark. It is available for a variety of platforms. For this example, I'll be installing it on Ubuntu Linux. To do that, we can simply use the `apt` tool:

```bash
sudo apt update
sudo apt install wireshark
```

When you install Wireshark, you may be shown a message about installing Dumpcap in a way that allows members of the `wireshark` group to capture packets. Press <kbd>ENTER</kbd> to go to the next screen, then use the arrow keys (<kbd>&larr;</kbd> and <kbd>&rarr;</kbd>) to select `<Yes>` on the menu asking if non-superusers should be able to capture packets, then press <kbd>ENTER</kbd> to confirm that option.

After you install Wireshark, you'll need to add your current user account to the `wireshark` group. If you are using the `cis527` account, you can do the following:

```bash
sudo usermod -a -G wireshark cis527
```

Next, you'll need to log out and log in for the new group membership to take effect. Otherwise, you won't be able to directly capture packets unless you run Wireshark as `root`, which is not recommended.

Once you do so, you can search for "Wireshark" on the Activities menu to open the program. If you configured it correctly, it should show you all of your network interfaces on the first page. If you do not see them, check to make sure that your user account is properly added to the `wireshark` group and that you've logged-out and logged-in again.

To capture packets, we must first select which interface we'd like to listen to. Since I would like to capture packets on the actual network, I'm doing to select `ens33` from this list. Your network interface may be named slightly differently, but it should be obvious which one is the correct one. As soon as you do so, you'll start seeing all of the network packets sent and received on that network interface. By default, we are not listening in "promiscuous" mode, which would allow us to see all the packets on the network, regardless of the sender or recipient.

As you can see, even if you aren't doing anything on the network yourself, there is always a bit of background traffic. Many of these packets are from your system and others on the network performing simple network requests from several of the background services or daemons. Most of them can be safely ignored for now, but if you are concerned about malicious network traffic on your network, any of these packets could be suspect.

Now, let's see if we can capture some interesting network traffic. First, I'm going to open a web browser, and go to a simple web page. I'm visiting my old personal page on the K-State CS systems, since it doesn't automatically redirect me to a secure connection. That way we can see the contents of the packets themselves.

Now that we've done so, let's use the filtering features in Wireshark to see those packets. First, I'm going to press the "stop" button at the top to stop capturing packets. Next, I'm going to enter `dns` in the filter and press <kbd>ENTER</kbd> to only show the DNS packets in the output. There are still quite a few of them, but after scrolling through them I should see the ones I'm looking for.

Here I've selected the first packet I sent, which is a standard DNS query for `people.cs.ksu.edu`. Below, I can see all of the layers of the packet. The top layer shows the frame from the Physical and Data Link layers. Below that, we see the Ethernet protocol information from the Data Link layer. By expanding that, we can see the source and destination MAC addresses of the this packet. Going further, we can see the Internet Protocol Version 4 header from the Network layer, which gives the source and destination IP addresses for this packet. Note that the original destination was the default gateway, which is also the DNS server I've configured this system to use.

We can also see that it used the User Datagram Protocol in the Transport layer. Here, we can see the source and destination ports. Notice that the source port is a very high number, meaning that it is most likely an ephemeral port on this system, whereas the destination port is 53, the "well-known" port for the DNS application layer protocol.

Finally, we can see the contents of the DNS packet itself. If we look inside, we can see the query for `people.cs.ksu.edu` inside the packet. This view helps you clearly visualize the layers of encapsulation that each packet goes through as it makes its way across the network.

A couple of packets later, we can see the response to the earlier query. Going back through each layer, you can see the source and destination MAC address, IP address, and port numbers are all reversed, just as you'd expect. Finally, looking at the contents of the DNS packet, we can see the response includes an answer for the query. Here, it shows that `people.cs.ksu.edu` is a `CNAME` or "canonical name" record, which points to `invicta.cs.ksu.edu`, the actual server it is stored on. Thankfully, DNS will also give us the IP address of that server, which is the second record, an `A` or "address record," in the response. We'll discuss these DNS record types in a later video.

Depending on your browser's configuration, you may also see additional DNS queries for the each URL included on the page that was loaded. For example, here I see queries for `projecteuler.net`, `russfeld.me`, and `beattieunioncemetery.org`, which are all linked at the bottom of my page. Most browsers do this as a way to speed up subsequent requests, as they assume you are likely to click on at least one of those links while visiting that page. Since it has already done the DNS query, it is one step closer to loading that page for you. In fact, many browsers may already send requests to that server in the background and have the page cached and ready to go before you click the link.

This is a very brief introduction to the power of Wireshark and how to use it to capture packets. Over the next few videos, we'll explore some Application layer protocols and use Wireshark to help us explore the packets for each one. In the meantime, I encourage you to play around a bit with Wireshark and see what sorts of packets you can see on your own.
