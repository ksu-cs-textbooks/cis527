---
title: "Fall '25 Week 9"
weight: 20
pre: ""
---

{{< youtube NRjtZE-PUUY >}}

#### Resources

* <a href="slides" target="_blank">Slides</a>

#### Video Script

Hello, and welcome to the week nine announcements video for CIS527 and CC510 in fall 2025. So this week you should be working on getting lab 4 finished up. Because we had all the outages yesterday, I've moved the lab 4 quizzes to tomorrow, which is Wednesday. Today we have our third discussion, which will be today at 2.30 that I'll talk about briefly. Lab 4 is due this Friday. And then next Tuesday, we're going to have our second discussion that I will also talk about briefly. So the schedule is a little weird. Hopefully it all makes sense. And all of these dates should also be accurate on Canvas. 

So this week you're working on Lab 4. We've talked about it a little bit already. Basically, the big idea is to add an Active Directory and Open LDAP to your Ubuntu and Windows systems and then configure the clients to log in via those systems. Make sure you read the instructions very carefully, make snapshots where I tell you to make snapshots. And of course, if you have questions, either post on Ed Discussion or email the cis527-help and we would be happy to help you out. 

So there are three different ways you can do Lab 4 setup. If you have a working Lab 3, you can use your Lab 3 DNS and DHCP servers. Those work great. The only thing I usually recommend is on the Windows client or the Ubuntu client that is pointing to the Windows Active Directory that you add the static DNS entry to point to the Windows server instead of the Ubuntu server. That seems to fix a lot of problems with Active Directory. If you don't have a working one, you can do static DNS entries or host file entries. There is a network setup document that talks about some of this. If you have questions or have trouble getting the Lab4 network set up, let me know. I'd be happy to help. 

So Lab 4 grading is pretty straightforward. We just want to see that your Active Directory server is set up, has the correct user and group on it, and that your Windows machine can log in with Active Directory. Then on Ubuntu, you're going to have an Open LDAP server with a user and group on it. And then you'll have an Ubuntu client that logs in via LDAP and an Ubuntu client, either another VM or another snapshot of the same VM that can log into Active Directory. If everything's working, takes less than five minutes to grade. If things are not working, it's kind of frustrating to debug, but we will do the best we can to see where you're at in the process and try and give you partial credit for as far as you got. 

So then after that, we're going to switch to Lab 5. Lab 5 may not be published yet on Canvas, but I'm going to get it published very soon. Lab 5, we're going to move out to the cloud. We're going to create some droplets on DigitalOcean. We're going to set up SSH and firewall on those droplets. And then we're going to set up some websites, DNS, and we're also going to play a little bit with Docker. I think Lab 5 is a little bit simpler than Lab 4. Generally, it's much lower in terms of time requirements, but it's a good setup for the last couple of labs that we're going to do in this class. So this one, we're going to move to the cloud. 

One of the things you might want is the GitHub Education Pack, which you can find at education.github.com slash pack. There are some other things that you can find out there if you Google real quick. That second URL, it gets cut off. It's try.digitalocean.com slash free trial offer. That will get you $200 in free credits to DigitalOcean as long as you sign up a new account. You can also go to nc.me to sign up for a Namecheap account. I have referral links for both of those as well if you want those. So you can ask me for some referral links. Total cost to you at most, even if you have to pay for everything out of pocket, should be about $11. But with these trial links, everything should be cheap. I think the only thing you really have to pay for is the domain name, which should be 99 cents for the first year. Again, if you have trouble, let me know. I also know last year we had trouble with some students getting signed up on DigitalOcean that they got flagged as spam. If that happens, let me know. I've got some extra email accounts that we can use to sign you up to get you started. So just reach out to me anytime. But those are some of the resources you'll need for Lab 5. 

So we've got two discussions coming up. This week, we've got Nick Eggleston and Nathan Wells, our two BayoCat sysadmins. They're going to be speaking today at 2.30. So make sure you get your questions in for that. And then next week, we're going to have Kyle Hudson. He is the former BayoCat admin, also formerly at Canren, which is the ISP that provides internet to universities in Kansas, such as K-State. And he currently works at Lambda Labs. And he's going to be in next Tuesday at 2.30. So make sure you have your questions prompt for that. 

Other than that, feel free to keep in touch. I'm always available on Ed Discussion, Discord, Teams, Tea Time office hours, et cetera, et cetera. 

But hopefully things are going well. I had to include this XKCD comic, especially where we're moving into the cloud next week. And also, we had a big cloud outage yesterday. And so it's just important to remember that to you, it's the cloud, but to everybody, it's to somebody, the cloud is just somebody else's computer. Hopefully, it's more than just a box sitting in somebody's apartment with a single cable. But that's really the thing to keep in mind. So hopefully everything goes well this week. Best of luck. If you have any questions, let me know. Otherwise, I will see you again next week. 