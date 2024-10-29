---
title: "Fall '24 Week 7"
weight: 20
pre: ""
---

{{< youtube L4UNP32Oh54 >}}

#### Resources

* <a href="slides" target="_blank">Slides</a>

#### Video Script

Hello and welcome to the week seven announcements video for CIS 527 and CC 510 in fall 2024. This week you should be working on the response to our second discussion with Seth Galliser. Those responses are due today, so make sure you get those posted. And then this Friday, lab three is due. Hopefully you saw the announcement earlier that I have moved all of the lab deadlines to Friday. That seems to work better for Josh and I and our schedule. We have a lot more time for grading on Wednesday, Thursday, Friday. Please bear in mind, you can go ahead and schedule your grading time right now as long as you know you're going to have your lab done before that deadline. So if you want to reserve your time on Friday, go ahead and get it scheduled and we will take care of that. But just bear in mind that labs are now due on Fridays and then for the times when that conflicts I've moved things around. So just check the deadlines in Canvas because those are the accurate timelines for all of this. 

So for lab three, you should be working on setting up core networking services on your servers. Most of this is done on a single Ubuntu VM with a Windows and Ubuntu client VM for some testing. You're going to set a static IP address on your Ubuntu server. You're going to install DNS and DHCP, install SNMP. You're going to configure remote access on a couple of machines. Feel free to ask questions. I'm constantly fielding questions from students both in ed discussion via email and on Discord. I have a mega thread on ed discussion where I'm trying to consolidate all of the information that I get from all the different students I chat with. So feel free to check that out if you have any questions that might have a frequently asked question there that can answer some of your problems. But as always, don't be afraid to ask questions or let us know either meet with Josh or I and we can help you out. 

So for grading on lab three, the big things we're going to ask you to do are demonstrate your remote connections. So be prepared to show that you can use remote desktop from one of your Ubuntu clients into the Windows machine using Remina. Also be able to show that you can use SSH from either Windows or Linux to get into your Ubuntu server. You should know what those commands are and how to use them. Make sure you can show us your static IP is set on your Ubuntu server. So you'll just go into the. of the settings there. Be prepared to show us your DNS server settings. We're gonna ask you to look at all those config files that you created and then we'll have you run a few DIG commands to do some lookups. So make sure you're comfortable with that. We'll also check your DHCP settings and we'll check to make sure that your clients are getting DHCP addresses from your DHCP server. For the SNMP part and the Wireshark part, we're just gonna grade your screenshots. So make sure you have screenshots of the SNMP activity that we have you do and have screenshots of the eight different Wireshark packets that we have you capture and make sure it's really clear in those screenshots that you found the thing that we're looking for. Really, for a lot of this grading, I expect you, if everything goes well, to know how things work and you should be able to do these pretty quickly, we'll be prepared to prompt you if you're unsure. But let us know if you have any questions or concerns and we'll work with you from there. 

So for lab four, you're going to create a Windows Server VM, and we're going to set up Active Directory and open LDAP and configure the clients to work with those. We're also going to configure one instance of interoperability, where we'll have an Ubuntu client login to Active Directory, which is really cool. The big thing for this lab is to make snapshots as often as you can, especially when installing the Active Directory part of Windows Server, and when configuring the LDAP on Ubuntu, especially the security certificates, those tend to cause a lot of problems with students. So having a snapshot where you can roll back and try again is always helpful. For the few students that are going to do this in Azure, I'm going to get those videos hopefully posted in the next couple of days that give some basic ideas of how to set up virtual machines in Azure. If you want to work in Azure, you're welcome to. It does work really well for this. I was able to do the Windows parts of lab four in Azure pretty easily, so just be aware of that. But lab four is probably the more difficult lab. It's one of those that it either works or it doesn't, and so grading this lab is actually really simple. It either works or doesn't, but there's a lot of different gotchas and things that you could run into to get lab four working. Most students in the past have said that lab four is probably the most difficult. It's kind of tied between lab three and lab four, so just be aware of that. Start early, ask questions, let us know if you have trouble. 

So as always, I've said in this class, the big key to success is reading the labs carefully, looking at the posted hints and discussions. I'm always willing to give hints and pointers and help debug stuff. It's not that I'm going to tell you, oh, I don't know what the error is. I will help you. You just have to reach out and ask. Use the resources that are available. And the big thing I tell students is don't spin your wheels. If you've been debugging a problem for 20, 30 minutes, you haven't made any progress and you're not figuring anything out, that's a good time to take a step back, relax, ask us a question, send us some screenshots, and we'll help you figure it out. 

So that's really all I've got for this week. As always, feel free to keep in touch. We've got a great discussion going on. discussion. I'm on Discord. I'm on Teams. I've got office hours today for this class from 2 .30 to 3 .30. I have tea time office hours on Mondays if you want to chat about other stuff. And then, of course, you can always schedule a one -on -one time with either Josh or I, and we'd be happy to help you out. So best of luck as you wrap up Lab 3 and get started on Lab 4. If you have any questions, let us know, and I will see you again next week. 