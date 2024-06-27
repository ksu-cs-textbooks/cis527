---
title: "Fall '23 Week 9"
weight: 25
pre: ""
---

{{< youtube y6hyCDsHMlw >}}

#### Resources

* <a href="slides" target="_blank">Slides</a>

#### Video Script

Hello and welcome to the week nine announcements video for CIS 527 and CC 510 in fall 2023. This week Lab 4 is due tomorrow, so make sure you're getting Lab 4 all wrapped up. Then you should also be starting on the content for Lab 5, which is some introduction to the cloud. And then a couple weeks from now you'll have the Lab 5 content that's actually due, so you should get started on Lab 5 sometime next week. So for grading on Lab 4, basically we want to see a few simple things. We want to see your Windows Server up and running with an Active Directory installed and a static IP address. We want to see that you've created a user and group and Active Directory, and we want to show that you've connected a Windows client to that Active Directory. Then we'll shift over to Linux. We want to see that you've installed Open LDAP and you've created a user and group using LDAP Account Manager. I posted an announcements video yesterday with a video showing you how to install LDAP Account Manager, so hopefully that helps. I apologize for the bad audio quality on that video. It was recorded on my laptop, which doesn't have a good microphone. I will re -record a more professional version of that video in the future. And then we want to see you have an Ubuntu client that logs into LDAP using the LDAP client. We also want to have an Ubuntu that logs into your Active Directory. Those could be two different VMs, two different snapshots of the same VM. It's up to you how you want to handle that. But that's really all we want to see with Lab 4. If everything's working, it takes very little time to show us that it's working. If you have trouble, feel free to work with Matt or I, and we'd be happy to help you debug it. We're slowly getting better with debugging problems with Lab 4. 

So some quick reminders to be successful in this class. Make sure you read the assignments very carefully. Take a look at any posted diagrams or resources that I have. A lot of those resources have good steps, tutorials. Generally, I try and post them in the order of usefulness. So typically the top one that I post is the one that you're most interested in on the assignments. But if you're stuck, don't be afraid to ask questions. Don't be afraid to come to office hours. The big thing is don't spin your wheels. Don't feel like you just keep working in a rut. If you've been working on something, just keep working on it. for half hour and can't figure it out. Come talk to us, let us know. We've got some pretty good background in debugging and can do a lot to help you figure out what's going on. So feel free to reach out. 

So this week you should be moving on to Lab 5. Lab 5, we're going to shift over to doing some stuff in the cloud for Lab. We won't use the VMs for this lab, but you'll still need them for Lab 6 and 7, so hold onto those. If you're running out of storage space, let me know or let Matt know. We've got some tips we can give you to help resolve some of that. Basically what you're going to do is set up two droplets on DigitalOcean's cloud infrastructure. If you have experience with AWS and Azure, you're welcome to work there. I don't have a lot of experience with that or debugging anything there, so I really recommend DigitalOcean if possible, but you're welcome to do something else. Just understand if it breaks, I may not be able to help you fix it and I may ask you to move to DigitalOcean. You're going to set up an SSH in firewall, you're going to configure the Apache web server and some simple websites on Apache. You'll set up a working DNS name, and then we're going to do a little bit with... Docker and you'll set up a Docker reverse proxy to two different Docker containers just to get a little bit of experience working with Docker in lab five So one thing you can do is if you don't have any access to digital ocean yet You can either register for the github education pack at this URL You can also go to try that digital ocean comm slash free trial offer. I apologize that got cut off Usually digital ocean has an offer where you can get anywhere from 100 to 200 dollars in free credit with a new account Same thing for name cheap dot me you can get a dot me domain for 99 cents If you need credits on digital ocean, let me know I've got referral credits. I can give you as well Overall for this class the total cost you should spend on this is about 11 dollars. It's pretty cheap I think it's it's reasonable to do this on your own But most of these you can get for free or for 99 cents So hopefully it works should work out but at most you should pay no more than 11 dollars to complete some of this stuff 

So finally a quick reminder, I've got some upcoming travel this week I'll be out of the office Thursday through Sunday of this week because that responses be email and grading may be a bit delayed Matt is still available so you can reach out to Matt anytime if you have questions Please make sure you use the CIS 527 help email address that's on the canvas page or post an ed discussion Those go to both Matt and I so we can help you out there Finally, of course, there's opportunities to keep in touch. We have a discussion on discord. We have ed discussion boards We have time for one -on -one office hours Matt should be at the Thursday office hour time as well if you'd like to meet within there I'm working on scheduling the next discussions. Unfortunately. I've had to reschedule a couple of things So I'll be working on that soon We'll try and have at least two more discussions this semester My goal is to have three more but we'll see if we can fit that all into the schedule But those will be getting posted very shortly as well So we're getting up to the cloud It always reminds you of this great XKCD comic where the cloud is just somebody else's computer I think this really describes it quite well. So if you haven't seen this comic take a look at this XKCD comic I hope everything goes well with lab 5 if you have any questions, let us know and I will talk to you again in a couple weeks Good luck 