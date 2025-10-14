---
title: "Fall '25 Week 8"
weight: 19
pre: ""
---

{{< youtube 8nuwOtj5JZo >}}

#### Resources

* <a href="slides" target="_blank">Slides</a>

#### Video Script

Hello and welcome to the week 8 announcements video for CIS 527 and CC 510 in fall 2025. So we don't really have anything due this week, but next week on Monday are the quizzes for lab 4. Then next Tuesday we're going to have the third discussion with the current BayoCat sysadmins. And then lab four is going to be due a week from this Friday on the 24th. Then on Tuesday the 28th right before Halloween we're going to have our second discussion which is Kyle Hudson. But there's nothing available and nothing due this week. I just want you to get started on lab four and start working on that because it is one of the harder and more time consuming labs for this semester. So make sure you get started on that soon. 

Lab 4, you're going to create a Windows Server VM and then install a Windows Active Directory on that. You're also going to install Open LDAP on your Ubuntu server and then configure clients to connect to those. We're also going to play a little bit with interoperability where we're going to take an Ubuntu client and put it onto your Windows Active Directory, which is pretty cool. Unfortunately, we don't go the other way where we put a Windows client on Open LDAP. That's really difficult to do. But I do show you a video of what that looked like from a couple years ago. And then, of course, don't forget, make snapshots and use those. I give a lot of hints in the lab for times when you want to make snapshots. 

To get set up for lab four, you've really got three options. Ideally, if your DNS and DHCP server from lab 3 are working fully, you can go ahead and continue to use that lab 3 setup. Just make sure your Ubuntu server is always running in the background, providing that DNS and DHCP. If you didn't get those running, you can use a static DNS entries in your Lab 3 config. So basically, your Ubuntu talks to your Lab 3 DNS server. Your Windows talks to your Windows server for DNS. So you can do some of that. And then if that doesn't work, you can also set static host file entries. Generally on Windows, especially, you want to set a static DNS address that points directly to the Windows server so that the AD works. And then same thing when you're setting up an Active Directory on Ubuntu, set that so that the DNS server points to the Windows server. Everything works great. If you have any questions on Lab 4 setup, let me know and I'm happy to help. 

So for Lab 4 grading, this one's pretty straightforward. We check and see if your Windows server is installed and you have an Active Directory user and group setup and then that your Windows client logs in on AD. Then we go to your Ubuntu server, check that LDAP is installed, has a correct user and group in it, and then you have an Ubuntu client that logs in via LDAP and another Ubuntu client or another snapshot of an Ubuntu client that logs in via Active Directory. That's all it is. 

So we've got two speakers coming up. Next Tuesday, we have Nick Eggleston and Nathan Wells, our two current BayoCat sysadmins. So make sure you're thinking of questions for them. And then two weeks from that, two weeks from today is going to be Kyle Hudson, who is a former BayoCat admin and now currently works at Lambda Labs. 

Other than that, feel free to keep in touch. There's a lot of stuff going on. If you haven't already, please register and attend Hack K-State if you're available this weekend. It is in the business building. It's a great chance to hang out with computer science students and either do your homework and get free food or actually do a hackathon project and get free food. So feel free to hang out with us this weekend at Hack K-State. I should be there most of the time. So I look forward to hopefully seeing some of you there. Other than that, we're at the halfway point of the semester. Hopefully things are going well. Best of luck this week. And I will see you again next week. 
