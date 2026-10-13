---
title: "Fall '26 Week 8"
weight: 19
pre: ""
---

{{< youtube 07-V2FebxAw >}}

#### Resources

* <a href="slides" target="_blank">Slides</a>

#### Video Script

[00:00]
Hello and welcome to the week 8 announcements video for CIS 527 and CC 510 in fall 2026. So coming up, we've got the discussion to response that's due pretty soon this week, so make sure you get that turned in and updated. I believe that's due on Thursday. The Lab 4 quizzes are due on Friday. Next week on Wednesday, we have our third discussion session, which I'll talk about briefly. And then at the end of that week, Lab 4 is due. So you should hopefully be starting on Lab 4 soon.

[00:31]
Lab 4, you're going to add a Windows Server VM and configure Active Directory and LDAP. You'll also configure clients and some interoperability on that lab. Big advice I can give you on this lab is to make snapshots, especially before you promote a Windows Server to an Active Directory client, before you configure OpenLDAP, and before you configure SSL in OpenLDAP. All of those tend to cause issues, and so make sure you make those snapshots just so you can roll back in case you have any problems. So for Lab 4 setup, there are three different options. If you take a look at the textbook, there is a page that shows some networking diagrams. If you're confident with your DNS and DHCP server from Lab 3, you can continue to use those in Lab 4. You can also set up static DNS entries in Lab 3, and you can actually set up host file entries for Lab 3 as well. So if you don't have your DNS server working, you can set up some static DNS entries as well. Doesn't really matter as long as you can get everything to work and as long as each machine can find each other. If you have any questions on this setup, let me know. Hopefully your DNS is working, but if not, feel free to reach out.

[01:33]
Another big thing to bear in mind is for Lab 4, those of you that are using ARM platforms, so specifically the Apple M2 chips, M1 chips, those things, unfortunately, Windows Server does not have a virtualized version on ARM right now. They had a demo version and it is no longer available. For this lab, you'll need to use Azure for the Windows Server portion of this lab. You'll also use it again in Lab 6, so be aware of that. There is a textbook page with a video that goes through the process of setting up an Azure virtual machine for Windows Server. That video, I believe, should be current. If you see anything different or anything that doesn't make sense as you walk through that video on Azure, let me know, and I'll go through the process again on my end and make sure that they haven't changed anything since I recorded that video. But that's the big thing to be aware of. And so for Lab 4, you'll kind of have a split setup where you'll have your Ubuntu stuff locally and your Azure Active Directory stuff in the cloud should hopefully be pretty straightforward to do.

[02:29]
For Lab 4 grading, this one's actually pretty simple. We're just going to check and make sure that your Active Directory and OpenLDAP is set up, it has the correct users and groups on it, and that you can connect the clients to the appropriate system. So Windows will connect to AD, and then you have an Ubuntu that connects to LDAP and another Ubuntu, usually a snapshot of the same VM, but it could also be a separate VM that connects to Active Directory. That's what we're really looking for Lab 4.

[02:56]
Also coming up next week is our third speaker session. The speaker this time is Kyle Hudson, one of my favorite speakers to bring in this class. Kyle currently works at Lambda. I believe they've changed their name now to just Lambda instead of Lambda Labs. He previously worked at KANREN, which is the internet service provider for K-State, and formerly was a Beocat sysadmin for about 10 years. Kyle is an immense expert on high-performance computing. He tells some of the best stories about high-performance systems. So I encourage you to come join that session. He's going to be with us on Wednesday the 21st at 2 30 p.m via the usual Zoom link. Usual rules apply. Submit a question beforehand so you get points for that and then either attend the live session and ask a question or do the response afterward to get points for that. Other than that, hopefully things are going well. We're at the halfway point of the semester so if you have any questions feel free to reach out on Ed Discussion, come to office hours, find me on Teams, anything like that, and I would be happy to help. Otherwise, best of luck, and I will see you again next week.