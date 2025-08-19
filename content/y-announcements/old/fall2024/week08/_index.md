---
title: "Fall '24 Week 8"
weight: 25
pre: ""
---

{{< youtube G1qY2UWUr9g >}}

#### Resources

* <a href="slides" target="_blank">Slides</a>

#### Video Script

Hello and welcome to the week 8 announcements video for CIS 527 and CC 510 in fall 2024. So coming up we're working on lab 4 so by next Monday you should have the quizzes done for lab 4 and then by next Friday you'll be turning in lab 4 itself. This really this couple of weeks this is probably the hardest part of this class I know a lot of students struggle with getting lab 4 up and running not necessarily because it's difficult but because there's a lot of bits and pieces to deal with and there's a lot of dependencies that you have to work around as well. So those are all things to keep in mind. 

So like you've seen before lab 4 involves creating a Windows Server virtual machine and installing Active Directory on it. We're also going to install the open LDAP server on our Ubuntu system. We're going to configure clients to log in through those systems so we'll configure Ubuntu to log in through LDAP and we'll configure both a Windows and an Ubuntu to log in via Active Directory. That's really all it is. One thing I definitely will tell you to do is make snapshots in this lab especially before you configure Active Directory on Windows and before you configure open LDAP and the TLS part of open LDAP on Ubuntu. Those are two steps that might cause you issues and so having a snapshot you can roll back to is really really useful. 

So for the lab 4 setup there are a couple of different ways you can do lab 4. I have a document in the textbook that describes this but there's basically three options. If you have a working lab 3 solution and you want to keep working on it you can continue to use the lab 3 DNS and DHCP server and it should work well for all of this. The only thing you really have to do on lab 4 is on the Windows client you have to set a separate static DNS address to point to the Windows server. If your DHCP is not working but you want to use your DNS you can use your DNS server from lab 3 as static DNS entries or the third option and this is usually what I recommend if you're not so sure about your lab 3 setup is to set up manual hosts file entries. I'm gonna try and record a video for that later today or tomorrow and post that out there so you can see what I mean when I talk about that setup but there's really three different ways that you can set up lab 4. so that the Active Directory and OpenLDAP parts will actually work correctly. 

So for grading on Lab 4, this lab is actually really easy to grade. It either works or it doesn't for the most part. So we're gonna check that your Windows Server is installed, that you have a user and a group in your Active Directory, and then we'll double check to make sure your Windows client can log in using your Active Directory. On the Ubuntu side, we're gonna check that you have OpenLDAP installed. We're gonna look at the LDAP account manager to make sure there's a user and a group configured there. And then you should have an Ubuntu client that logs in via LDAP and an Ubuntu client that also can log in via the Active Directory. Those may be the same client with two different snapshots. Either way you wanna do that is fine. But most of the point of this lab is if your clients can log in via the appropriate AD or LDAP server, that's what we're looking for and you'll get the points for this lab. 

So that's really all I've got going on this week. So as always, there's gonna be a mega thread on ed discussion if you have any questions there. You can ping me on Discord and Teams. You can come to Office Hours. I'm really here to help. I'm also going to be trying to schedule a couple more discussion sessions over the next month. So be on the lookout for that as I get those schedules posted. I just need to hear back from a couple of speakers to see what days work best for them. We're going to try and get at least two more, maybe three more scheduled this semester, depending on if the scheduling works out for everybody. So we're at the halfway mark of the semester. This is week eight. Hopefully things are going well. For most students, they point at lab four is one of the more difficult labs in this class. After this, we're going to switch gears a little bit and do some other stuff. So hopefully everything goes well with this lab. But as always, if you have any questions, let us know. And I will see you again next week. 
