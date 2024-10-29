---
title: "Fall '24 Week 9"
weight: 26
pre: ""
---

{{< youtube PLgcUKJvz3M >}}

#### Resources

* <a href="slides" target="_blank">Slides</a>

#### Video Script

Hello and welcome to the week nine announcements video for CIS 527 and CC 510 in fall 2024. I'm coming to you this week from my office on campus because I'm on the road a little bit. Hopefully the video quality is not too bad and you can get everything that I need to get across in these announcements. So for this week you should be working on lab four. Lab four is due this Friday so make sure that you're getting that done and have your grading time scheduled. Right now I have a lot of availability on Friday and I believe Josh should also have availability toward the end of the week so hopefully you can get your grading time scheduled. If you're having any questions or issues with the lab let us know and we'll definitely work with you on that and then next week you'll transition over and start working on lab five. 

So for lab four the grading for lab four is actually really straightforward it kind of just works or it doesn't. What we're going to look at is that you've installed a Windows Server and configured that with an Active Directory that has a user and a group in it as directed and then you should configure a Windows client to log in using that Active Directory. On the Ubuntu side of things you should on your Ubuntu server install OpenLDAP and have it configured with the user and group through the LDAP account manager and then you should have an Ubuntu client logs in via LDAP and then another Ubuntu client which could be either a different VM or a different snapshot of the same VM that then logs in via Active Directory. That's what we're looking for for lab four. Generally if it works we just check that your server has AD you show us that you're logged in check that OpenLDAP is running and show us that you've logged in on both Ubuntu's that's really all it takes. If everything is configured and running takes less than five minutes if you're having issues with it then we'll have to dig in a little bit and figure out exactly what's working and what doesn't so we can at least get you some partial credit. So as always success in this class involves reading the assignments carefully looking at the posted diagrams. I just posted a video last week showing some network setups for lab four including how to set things up in Azure so take a look at those videos and ask me if you have any questions. Use the resources that are available especially in the lab I usually link right below a task in the lab I link the resource that I use to do those tasks and finally if you get Don't spin your wheels if something's not working and you're not sure stop and ask us a question Post on a discussion email us post on discord, whatever Josh And I will try and answer as soon as we can And it's much easier to maybe get the right answer than to spin your wheels and try a whole bunch of things Especially unless you're very careful and have a snapshot in VMware that you can roll back to in order to get things working again.

So for lab 5 coming up next week, we're gonna move totally into the cloud for some of this class What I normally do with this class is build droplets in digital ocean I find the digital ocean is the easiest to use cloud platform for this We'll set up SSH and firewall although we'll need to make a couple of changes to that because campus is now blocking SSH So I'm working on getting that lab updated Then we're gonna set up some simple Apache websites a DNS domain name And we're also going to play a little bit with Docker instead of a Docker reverse proxy Notta Notta Notta So, Lab 5 is generally a little bit smaller than Lab 3 and 4. It's much more straightforward. It's working in the cloud, in DigitalOcean, in a couple of droplets. If you want to do Lab 5 on a different cloud provider such as AWS or Azure, you're welcome to do that. I will just warn you that I don't have as much experience with those platforms versus DigitalOcean where I host my own stuff and so I find it a little bit easier to debug and work on things in DigitalOcean versus those other platforms but really you can go any way you want. 

For this lab you'll need to set up a DigitalOcean account and you'll also need to set up a domain name if you so choose. You can get all of this through the Education GitHub Pack. DigitalOcean also has a free trial offer that URL gets cut off but it's try .digitalosion .com slash free trial offer or if you just google it. Likewise if you go to nc .me you can get a .me domain for $1. So both of those are really great. I also have credits that I can share on these and so if you want my referral link for either of these just let me know. I'm happy to share that with you. In total if you even have to pay for this out of pocket it should cost you about $11, a dollar for the domain name and $10 on DigitalOcean but most of this you should have more than enough free credits to do this. You can also use an existing domain name if you have one or contact me if you don't want to set up your own domain name and I can set you up as a sub -site under the cis527 .org site that I own so that you can work with it from there. 

That's really all I've got for this week. I'll spend a little bit more time next week talking more in depth about lab 5 but in the meantime if you have any questions keep in touch on id discussion on discord teams come to office hours and let us know how we can help. So next week we're really going to start leaning into the cloud. I always remember this particular xkcd comic that talks about the cloud. We'll get into this a little bit next week in my lectures but really the cloud is just a point of view it's just somebody else's system and so in theory the entire cloud could just be some server in somebody's basement with a lot of caching. So I really like this xkcd comic it gets the idea across. So hopefully everything goes well this week. As always if you have any questions let us know and I will see you again next week. 