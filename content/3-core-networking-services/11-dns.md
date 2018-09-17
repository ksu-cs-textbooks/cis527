---
title: "DNS"
weight: 55
pre: "11. "
---

{{< youtube CN8YPR_X1eU >}}

#### Resources

* **[Slides]({{< relref "/3-core-networking-services/11-dns-slides.md" >}})**
* [Domain Name System (DNS)](https://en.wikipedia.org/wiki/Domain_Name_System) on Wikipedia
* [List of DNS Record Types](https://en.wikipedia.org/wiki/List_of_DNS_record_types) on Wikipedia
* [Domain Name System (DNS) History](https://www.livinginternet.com/i/iw_dns_history.htm) from Living Internet
* [BIND](https://en.wikipedia.org/wiki/BIND) on Wikipedia
* [HOSTS.TXT](https://jim.rees.org/apollo-archive/hosts.txt) from March 22, 1985
* [Root Name Server](https://en.wikipedia.org/wiki/Root_name_server) on Wikipedia
* [Root Files](https://www.iana.org/domains/root/files) from IANA
* [How To Configure BIND as a Private Network DNS Server on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-configure-bind-as-a-private-network-dns-server-on-ubuntu-18-04) from DigitalOcean
* [Bind9 Server How-To](https://help.ubuntu.com/community/BIND9ServerHowto) from Ubuntu Community Help Wiki
* [DNS Configuration](https://help.ubuntu.com/lts/serverguide/dns-configuration.html) from Ubuntu Server Guide
* [BIND Manuals](http://www.bind9.net/manuals) from bind9.net

#### Video Transcript

The Domain Name System, or DNS, is another integral part of working with the internet and larger networks today. In this video, we'll cover the history of DNS, how it works, and how to use it in an enterprise organization using the BIND software.

As a quick note, much of the information in this lecture is adapted from information provided by Seth Galitzer, our system administrator here in K-State CS. He created the original slides as part of a guest lecture in this course when it was offered on campus, and was gracious enough to share this information for future versions of the course.

First, let's review some quick history. As you may know, the precursor to today's internet, the ARPANET, was first conceived in 1965. By 1969, the first four nodes of that network were connected. Over the next two decades, ARPANET slowly grew in size, and by 1982, with the introduction of TCP and IP, it exploded in size as various networks joined together to create the internet we know today.

In the early days, they found it would be helpful to have a list of human-readable names for the nodes on the network. In that way, instead of remembering the IP address of a particular server, you could just remember its name and look up the IP address, much like you would look up the phone number of a person or business using a phone book. So, they created a file called `hosts.txt`, which was hosted by the Stanford Research Institute. In essence, it contained a list of all of the servers on ARPANET, paired with its IP address. Anyone could query that file with a computer name, and get back the IP address of the system.

While it was a useful system, it had some major drawbacks: first, it must be updated manually. At one time, the only way to add a new system to the file was to contact the person in charge of it via telephone. As the file grew larger, it was more and more difficult to maintain consistency and avoid name collisions. Finally, it became very taxing on SRIs system, as each system on the growing internet would download a copy of the `hosts.txt` file to store locally, sometimes requesting it many times per day to get the very latest version of the file. So, a new system needed to be built to provide this feature.

In 1983, the first version of the Domain Name Service, or DNS, was published as an RFC. It was later finalized in 1987. They proposed creating a distributed system of name servers, as well as a hierarchical, consistent name space for all the systems on the internet. Beyond just working with domain names and IP addresses, they also added the ability for the system to work with many different protocols and data types, hopefully designing it in such a way that it would work well into the future. Thankfully, their design was very successful, and we still use it today.

The domain name space we use today has a hierarchical format, much like this diagram. At the very top of the diagram is the root nameserver. It is responsible for keeping track of the locations of the DNS servers for all top-level domains, or TLDs, in the current domain name space. The original DNS specification calls for 13 root name servers, which is still true today. However, due to advances in technology, there are nearly 1000 redundant root name servers on the internet today, each one a clone of one of the 13 root servers. The file containing information for all of the top-level domains is very small, only about 2 MB, and can be viewed by following the link in the resources section below this video.

Below the root name server is the name server for each chosen top-level domain. For example, these are nameservers for the `.com`, `.org`, `.edu` and other top-level domains. Under each top-level domain are the name servers for each individual domain name, such as `yahoo.com`, `slashdot.org`, or `k-state.edu`. Within each domain, there can be additional levels of delegation, such as the `cs.k-state.edu` subzone, maintained within the K-State CS department for our internal systems.

With the hierarchical design of the domain name space, it may take a few steps to determine the appropriate IP address for a given domain name. For example, if you wanted to find the IP address of `www.wikipedia.org`, you might first start by querying the root name server for the location of the `.org` name server. Then, the `.org` nameserver could tell you where the `wikipedia.org` name server is. Finally, when you ask the `wikipedia.org` name server where `www.wikipedia.org` is located, it will be able to tell you since it is the authoritative name server for that domain. In practice, often there is a caching DNS server hosted by your ISP that stores previously requested domain names, so you won't always have to talk directly with the root name servers. This helps reduce the overall load across the root servers and makes many queries much faster.

The most commonly used DNS software today is BIND. BIND was originally developed in the 1980s as the first software to fully implement the new DNS standard, and it has been constantly under development ever since. The latest version of BIND is BIND 9, which was first released in 2000, but still consistently gets updates even today.

The DNS specification includes many different types of records. The most commonly used ones are listed here. For example, an `A` record is used to list a specific IPv4 address for a host name, whereas a `CNAME` record is used to provide an alias for another domain name. For this lab assignment, you'll be configuring a DNS server using BIND within your network and using several of these record types, so let's take a look at how that works.

Here I have configured an Ubuntu VM as directed in Lab 3 to act as a DHCP and DNS server. I also have a second Ubuntu VM acting as our client. Finally, I have disabled the DHCP server in VMware on this network segment.

First, on my server, I'm going to start Wireshark so we can capture these packets. I'll also add a filter for `dns` to make sure we only see the DNS server packets.

On the client, I have already verified that it is configured to use the other Ubuntu VM as a DNS server. You can see the currently configured DNS servers using this command:

```bash
systemd-resolve --status
```

At the bottom of that output, it should show the current DNS server for your ethernet connection. You'll have to press <kbd>Q</kbd> to close the output. To query a DNS record, we can use a couple of different commands. First, we can use the `dig` command to lookup a DNS name:

```bash
dig ns.cis527.cs.ksu.edu
```

Looking at the output received, we can see that we did indeed get the correct IP address. We can also run that command for `win.cis527.cs.ksu.edu` and `ubu.cis527.cs.ksu.edu`. Note that the output for `ubu.cis527.cs.ksu.edu` includes both the `CNAME` record and the `A` record.

To perform a reverse lookup, we can use the `dig -x` command. Since my sample network is using the `192.168.40.0/24` subnet, I could look up the following IP address:

```bash
dig -x 192.168.40.41
```

It should return the `PTR` record associated with that IP. I can do the same for the IP address ending in `42` as well.

On a Windows computer, you can use the `nslookup` command without any additional options to perform both forward and reverse DNS lookups.

Back on the server VM, we should clearly be able to see the DNS packets in Wireshark. Each one gives the type of record requested, and just below it is the response packet with the answer from our DNS server.

With that information, you should be ready to configure your own DNS server. As always, if you have any questions or run into issues, please post in the course discussion forums on Canvas. This process can definitely be frustrating the first time you do it, since there is so much new information to read and understand. Don't be afraid to ask for help if you get stuck!
