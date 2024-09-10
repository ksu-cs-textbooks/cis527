---
title: "Lab 3 Demo"
weight: 90
pre: "18. "
---

{{% notice warning %}}

This is for an older version of Lab 3, but the basic idea is the same. You may have to update some details such as the network IP addresses and hostnames to match the current instructions for Lab 3.

{{% /notice %}}

{{< youtube 1qBSikLyIRE >}}

#### Video Transcript

Okay, so I'm going to try and talk through a model solution version of lab three and give you some advice on how to go about this lab. And also how to verify that you got this lab configured and working properly. So the first thing we're going to do is we're going to look at our IP address. So I'm going to go to the Edit menu in VMware and then choose virtual network editor. And in the virtual network editor, we're going to find our NAT network. And we'll notice that it has a subnet address of `192.168.40.0`, yours will probably be similar, but it may have a different third octet right here. It's usually randomly assigned by VMware when you install it. Mine is dot 40. Yours might be different, so we need to make note of that IP address. The other thing in here we can see is this checkmark the use local DHCP service; once you get done with task four and have your DHCP server running, you'll want to go in here and uncheck this box, you have to click this change settings button to give it admin access. But then you can uncheck this box to turn off VMware's DHCP service, so you can use your own. So remember we have `192.168.40`. 

So up here in Ubuntu, we want to set a static IP address in that same range. So in my settings, if I go in here and look at IPv4, you can notice that I've set an IP address `192.168.40.41.` And the dot 41 is what the assignment says that we're going to use for our Ubuntu server. We also need to set the gateway. In VMware, it uses a default gateway of dot two inside of your network. The reason it does this is dot one is usually used by your home routers and some other services. And so to avoid any conflicts, VMware has set it to dot two. We also have the netmask of `255.255.255.0`. That's pretty standard. We talked about the lecture. And then you notice that right now I've actually set it to refer to itself as a DNS server. Originally in the lab, you'll probably set this to dot two, so that you still have working internet. But once you get your DNS server working, you can set it to dot 41. So that actually refers to itself for its DNS. So we'll go ahead and apply this once you apply it, you can turn it off and turn it back on to make sure it's applied. 

This is the only VM in this lab that you need to set a static IP address on. I've seen some students try and set static IPs on the Ubuntu and the Windows, you don't need to do that. For testing of your DNS server, you can set a static DNS entry temporarily. But the idea is by the time you get done with lab three these to your Ubuntu client and your Windows client should both be getting its IP address from the DHCP server on your Ubuntu server. 

Okay, so once we have that set, we can confirm our IP address is correct by doing `ip addr show` that will show us our IP address. And we'll notice right here that we see the 40 dot 41 IP address. We also need to keep in mind this `ens33`. This is the name of the interface that this is connected on. And so in the DHCP setup, you'll need to go in and set a file that defines which interfaces to listen on. This is the interface we want to listen on. But for the DNS server, we actually tell it the IP address that we want to listen on. And so we'll need this IP address in our DNS server configuration. 

So once we have our DNS server up and running, we'll also need to make sure that we allow it through the firewall, I'll leave that up to you, you can look up what ports you need and how to allow that through the firewall. 

But if it's working, we can use the `dig` command followed by an at symbol and the IP address of our system. And so what this does is this tells `dig` to ignore any DNS settings we have on our system and query this particular server, and we're going to query for `ns.cis527russfeld.cs.ksu.edu`. And when we do that, we get this response. Here, just to help. Let me put this command back up here again. So I'm doing `dig` at the IP address of my server. And you can do this either on the server or on the client. And then I'm giving it the name of a server that I want to look up in our DNS configuration. And so if I run this command, in this answer section, I should get back that this name goes to this IP address, which is correct. So that's how we look up an entry on our forward zone. 

If we went to look up an entry in our reverse zone, instead of doing the name, we do dash x, and then we would put in an IP address, I'm going to put in the IP address `42` which when we do this, it will show our answer section is we're looking up `42.40.168.192.in-addr.arpa`, which is the reverse lookup IP address. And then we are getting our Windows Server back.

So to really check to see if your DNS server is working, those are the two commands you need. You just need to be able to use `dig` at your server's IP address, and then dash x for reverse lookup, or for forward lookup, you just put in a domain name. You can also test your forwarding. If you want to make sure your forwarding is working, I can `dig` that server and just look for `www.yahoo.com` for example, and I can get responses from that. I can also look up the reverse. If I want to look up a reverse, I can do a reverse for `208.67.222.222` which is one of the OpenDNS resolvers. So this is pretty much confirmed that our DNS server is working on the server. 

If you want to check it from one of your clients, you can switch over to your client, and here on the client I can run those exact same commands. So if I do `dig` at my server IP address, and this is without setting any static DNS entries, this is just telling `dig` to query this IP. And then if I do my address here, then I can run it. And once again, we're getting that answer. And so this is how you can check, you can test your DNS configuration before you have DHCP working, you don't have to change anything on your client, you just use the at symbol in your `dig` command to tell it to query that particular DNS server for this entry. 

So that's the DNS parts. If that doesn't work, there's a really good guide on DNS troubleshooting that talks you through a lot of different things you might run into, Be especially careful of your periods and your spacing in your DNS configuration files. All of that is really important. There's also a really good discussion on Piazza right now about the number of octets in your reverse zone file. In the dot local file, you can have three octets and then you only need one octet in your zone file. If that doesn't make sense post on Piazza, let us know. We can try and clarify that. 

Okay, so the second part is your DHCP server. And the DHCP server configuration is pretty simple. However, I'm going to call out one thing real quick. If I go to `/etc/default`, you'll notice there's a file in here that might exist. That's, whoops. Helps if I go to the server. I go to the server. And then looking here, you'll see there is a file called `isc-dhcp-server`. And so in this file, it has some entries. And depending on what guide you read, sometimes you will need to define an interface right here that your DHCP server could listen on. Mine I didn't need to define that, it just worked. But in a lot of cases, you might need to define that. So this is where you would put that is that ens33 that we saw earlier. 

So once you get your DHCP server running, you can start it, I'm just going to restart mine. So I restart that. And now your server should be running. If you want to check, a good way to check is you can do `sudo cat /var/log/syslog`. And we'll look at the very end of our syslog. These last few entries. And we can see here that our, that our DHCP server started up; it read its config file. And then it will say things like listening and sending. And as long as you see that it's listening on `ens33`. That means it's working. If you get an error here that says it doesn't, it's not configured to listen on any interfaces, that's where you might need to change that defaults file to listen on ens33 to work. So. That's how you can tell your DHCP server started correctly. 

There's a couple other commands that you can use using the `ss` command to look at listening ports. So `ss -l` will show you all the listening ports on your system. However, it's not very useful at all. So instead, we can try two different versions, I'm going to do `ss -l`, then I'm going to do `t` which will listen for TCP ports only. And then `n` which will show us the port numbers. So if I do `ss -ltn`, I will see really quickly that I have a DNS server listening right here on port `53`. That's what we're looking for for DNS. DHCP, however, is not TCP is UDP. And so if I look for UDP, I'll see a DHCP server listening here on every IP address on port `67`. And so there is the entry for your DHCP server. And so if you're not sure if your servers are running correctly, you can use `ss -ltn` or `ss -lun` and look for entries that end in `53` for your DNS server or `67`, for your DHCP server. 

You'll also notice that there is `161` for your SNMP server if you have that running. So this is kind of a really useful thing. You can also see your SSH server running on `22222`, and we'll see our HTTP server Apache running on port `80`. So a couple of quick commands. 

But the really easy way to test your DHCP server is actually on Windows. And so on Windows, I have no static IP address set. If I do `ipconfig /release`, that will release all of our IP configurations. And then I can do `ipconfig /renew` to force it to renew that IP address. And so it will think for just a minute and then it will come back and it should give us an IP address that has something within our range. It has dot two as the gateway. But the big giveaway is you can find this connection-specific DNS suffix, and it will contain your eID. That's the dead giveaway that you are getting a DHCP address from your DHCP server. And that's why it's actually really easy to test this on Windows. 

Now, if I do `ipconfig /all`, then it will show all the information. And you can see that it also is getting the DNS server for your network. And so it actually gets the right DNS server, it will also show you what your DHCP server is. So if you want to know where that IP address came from, you can find it here as well. And then, of course, we can use `nslookup` to look up different names on our network. So if I do `nslookup`, I can look that up. And if I do the reverse, I can get the reverse as well. So everything is looking really good here. 

The other thing you can do, obviously, for testing is on your Ubuntu client, you can do `sudo dhclient -r`, which will run the DHCP client and refresh. If I do `sudo dhclient -v`, you'll actually see it sending the DHCP discover. So it sends to discover, then we get an offer of this IP address from our server IP. And you can see that it works. 

So those are a quick overview of what lab three should look like when it's working correctly. The big things to do are get your DNS server up and running, and then test it here on your server using those `dig` commands with the at symbol on them. So if we go back through my history, we find some of these `dig` commands having the at symbol where we can query a particular DNS server and look up a particular address. Once you get that working, you can then test it from your client using that same syntax or you can just go ahead, get your DHCP server up and running, check the system log to make sure it's running. And then go to your Windows client, reboot it and make sure that it's getting an IP address from your system. And then you should be good to go. 

If it's not working, check your config files, check your firewall, make sure that it's listening on the right ports, or feel free to reach out on Piazza and let us know. So I hope this video was helpful. If you have suggestions or questions or anything else I can go over please let me know.

Good luck.
