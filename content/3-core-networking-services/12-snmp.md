---
title: "SNMP"
weight: 60
pre: "12. "
---

{{< youtube  >}}

#### Resources

* **[Slides]({{< relref "/3-core-networking-services/12-snmp-slides.md" >}})**
* [Simple Network Management Protocol (SNMP)](https://en.wikipedia.org/wiki/Simple_Network_Management_Protocol) on Wikipedia
* [MIB Reference](http://www.simpleweb.org/ietf/mibs/) from SimpleWeb
* [SNMPv2 MIB Reference](https://www.alvestrand.no/objectid/1.3.6.1.2.1.html) from Harald T. Alvestrand
* [An Introduction to SNMP (Simple Network Management Protocol)](https://www.digitalocean.com/community/tutorials/an-introduction-to-snmp-simple-network-management-protocol) from DigitalOcean
* [SNMP Agent](https://help.ubuntu.com/community/SNMPAgent) from Ubuntu Community Help Wiki

#### Video Transcript

In the next few videos, we'll take a look at few other important networking protocols that you may come across as a system administrator. The first one we'll review is the Simple Network Management Protocol, or SNMP.

It was first developed in 1988 as a way for system administrators to query information from a variety of devices on a network, and possibly even update that information as needed. Remember that, in 1988, this was well before the development of the web browsers we know today, so it wasn't as simple as using the web-based configuration interface present on most routers today. However, while most systems today support SNMP, it is primarily used for remote monitoring of networking equipment, and not as much for configuration as it was originally intended.

Over the years, there have been many different versions of SNMP developed. Each one includes a few different features. The first version, SNMPv1, is very basic. While it works well for some things, it only includes a plain-text "community string" for authentication, resulting in minimal security. SNMPv2 is a significant revision to SNMPv1, and includes a much more robust security model. However, many users found that new model to be overly complex, and a second version called SNMPv2c, for "Community" was developed without the new security model. Finally, SNMPv3 was developed to include better security, authentication, and a more user-friendly design. It is the only currently accepted standard, though many devices still use the older versions as well.

In SNMP, the data is presented in the form of variables. The variables themselves have a very hierarchical structure, so that similar types of data are grouped together. However, the variables themselves can be difficult to read directly, since each level of the hierarchy is denoted by a number instead of a name.

To help make the variables more readable, SNMP includes a Management Information Base, or MIB, to define what each variable means. Each individual device can define its own MIB, though there are some standards available for common types of data. You can find a couple of those standards linked below the video.

The SNMP protocol itself lists many different types of protocol data units, or PDUs, as part of the standard. For example, the `GetRequest` PDU is used to query a particular variable on a device, and the `Response` PDU would be sent back from the device. You'll be able to see several of these PDUs a bit later in the video when we use Wireshark to caputre some SNMP packets.

As mentioned earlier, one feature of SNMP is the use of a "community string" for authentication. In SNMPv1, the community string is a simple text identifier that you can provide along with your request. The server then determines if that community string has access to the variable it requested, and if so, it will return the appropriate response. However, since community strings are sent as plain-text, anyone who was able intercept a packet could find the community string, so it wasn't very secure. In later versions of SNMP, additional security features were added to resolve this issue.

Now that you know a bit about SNMP, let's see a quick example of how it works. Once again, I have configured an Ubuntu VM as directed in Lab 3 to act as an SNMP server and client.

First, on my server, I'm going to start Wireshark so we can capture these packets. Notice that I'm capturing packets on the loopback adapter, since I'll be using `localhost` as the server address. I'll also add a filter for `snmp` to make sure we only see the SNMP server packets.

Next, still on the server, we can query the data available via SNMP using a couple of different commands. First, I'm going to use the simple `snmpget` command to query a single variable. I'll tell the system to use SNMPv1 with the `-v 1` option, and the "public" community string with `-c public`. In this case, I'll query the system's uptime:

```bash
snmpget -v 1 -c public localhost SNMPv2-MIB::sysUpTime.0
```

In the response, we can clearly see the system's uptime. If we switch back to Wireshark, we can see that it captured an SNMP `GetRequest` PDU, followed by an SNMP `GetResponse` PDU. If you examine the packet, you'll see that it requested the variable `1.3.6.1.2.1.1.3.0`. You can refer to the MIB reference links below this video to confirm that it is indeed the correct variable. Since we installed the MIBs on this system, it will automatically translate those numerical variable names to their standard paths and vice-versa.

To see all the available SNMP variables on your system, you can try the following:

```bash
snmpwalk -v 1 -c public localhost
```

This command will result in thousands of lines of output, giving all of the variables available on the system. Looking at Wireshark, you can see each of those packets consist of a `GetNextRequest` PDU, followed by a `GetResponse` PDU with the answer.

Since it can be very difficult to find exactly what you are looking for using the `snmpwalk` command, you can use `grep` to search the output for a particular item. For example, to see all of the variables related to ICMP, I could do the following:

```bash
snmpwalk -v 1 -c public localhost | grep icmp
```

If I know the set of variables I'd like to query, I can also include them in the `snmpwalk` command, such as this example:

```bash
snmpwalk -v  1 -c public localhost IP-MIB::icmp
```

Either way, you should see the variables related to ICMP, which would be very helpful for the SNMP portion of this lab assignment.

That's a quick overview of how to use SNMP to query information about your system across the network. If you have any questions about getting it configured on your system, use the course discussion forums on Canvas to ask a question anytime!
