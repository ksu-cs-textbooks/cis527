---
title: "Fall '23 Week 3"
weight: 10
pre: ""
---

{{< youtube zbBaalmEUvc >}}

#### Resources

* <a href="slides" target="_blank">Slides</a>

#### Video Script

Hello and welcome to the Week Three announcements video for CIS 527 and CC 510 in Fall 2023. So this week lab One is due tomorrow by 07:00 P.m., so make sure you get that done. Remember, for the lab grading, you need to schedule an interactive grading time with either Matt, My, UTA or myself via calendar. Both of our calendars are open. You can schedule a time anytime. However, please bear in mind that most of the time you have to schedule a meeting at least 2 hours in advance. So don't wait until tomorrow afternoon because we may be all full. And then you'll have to schedule for Thursday so make sure you get that scheduled ASAP. The lab is due before 07:00 P.m. Just to account for some late stuff in case people schedule for after work. Also, don't forget that the Week Two quizzes are due next week. So on September 11 on Monday, make sure you get those done. And then lab Two is going to be due on September 20. We're also shooting on having a discussion around that same time as well and I'll briefly talk about that. 

So the discussion sessions have been set for Thursdays from one to 02:00 p.m.. Most weeks those will just be office hours while I will sit in zoom for a while and answer any questions and that may also be there as well. I have sent out speaker invites to get a few speakers from industry to come in and I'm hoping to schedule our first speaker soon, probably within the next couple of weeks. And so as soon as I get the first few speakers nailed down, I will post that schedule, and then I will update the assignments on canvas, where you can go in and ask a few questions beforehand and then also have the assignment afterwards, where you can get participation credit if you're not able to attend the live discussion. But for right now, the Thursdays are just office hours, so feel free to drop by anytime if you have any questions on the lab. 

So you're going to start working on lab two. Lab two is basically redoing lab One using Puppet. So what you're going to do is create two new virtual machines, reinstall the operating system, you're going to install the Puppet agent and you're going to make a snapshot. After you've done all of that, I highly encourage you to reinstall the operating system and run all of the updates for the operating system, it may take several times in both Windows and Linux to get all of the updates. Then install Puppet and then make your snapshot. It's really, really important that you remember to make your snapshot at that time before you've done any other setup so that you can write your Puppet Manifest and test it and then roll it back to that snapshot. Every semester I have somebody do this lab forget to make that snapshot, and then they ask me if there's any way to undo it, and I have to tell them, no. You get to reinstall your VMs, so make sure you remember to make that snapshot the Puppet manifest. You're just making a manifest file to create users files and do a few other things. Try and keep it very simple. In the videos, I show some ways that you can use Puppet Resource to query your system to see what the setup is currently. So, for example, you could manually add some of those users. Use Puppet Resource to see what that looks like and then trim down that output to create the user accounts that you want. 

I do have model solutions for these. The model solutions are less than 200 lines of code per operating system. It is possible to create one unified file that works for both operating systems, but in general, I recommend creating one for Ubuntu and one for Windows. They're going to be similar, but they'll have some differences, so it makes it a lot easier to keep track. In this lab, you can also use anything from the Puppet Library. There are a couple of times where I show you how to use different library things. If you do use a library from Puppet, make sure you put in comments at the top of your Puppet manifest. What library needs to be installed if you use the Utils Library or Standard Library or the Windows File Permissions Library, anything like that. So make sure you make note of that so that when we're grading those, we know that we need to install those. And finally, for lab two, the grading for lab two is done offline. So all you have to do is submit your two Puppet Manifest files via Canvas, and then Matt and I will go through and grade those after. The lab is due in a couple of weeks. So you don't have to schedule a grading time for lab two unless you want to. If you want us to go through it manually, we can definitely do that as well. So that's really all I've got for this week. It's a pretty short week. 

Hopefully things are going well. As always, if you have any questions in this class, you can keep up with us by joining the discussions on Edstem. You can also join Office hours on Thursdays. There's lots of different ways you can get in touch with both Matt and I. So just let us know if you have any questions. Otherwise, I hope things are going well. I know that it kind of feels like you have to do this lab again, but that's really the point, is to show you the benefit of doing this manually versus the benefit of doing this in puppet. So hopefully things go well with lab two. Let us know if you have any questions and I will see you again in a couple of weeks. 