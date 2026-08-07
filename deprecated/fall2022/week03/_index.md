---
title: "Fall '22 Week 3"
weight: 10
pre: ""
---

{{< youtube HGkI2xUftR4 >}}

#### Resources

* <a href="slides" target="_blank">Slides</a>

#### Video Script

Hello, and welcome to the week three announcements video for CC 510 in Fall 2022. Hopefully today you're wrapping up lab one, if you haven't already, make sure you schedule the time to meet with me to get that graded. That's due tonight by 7pm. And then we'll start launching into module two. The week two quizzes are due next Monday. And then lab two is due the week after that along with the second week's discussion, which is actually the first discussion for this semester. 

So for this semester, our first speaker is Seth Galitzer, I've got a video that I recorded about a year ago of Seth talking about some of his experience in system administration. He actually has a bachelor's degree from computer science at K-State. He's been our system administrator in our department since 2006. So over 15 years at this point, he manages all of our computer science systems, all of our labs, including all of the servers and all the research systems that we work with. Seth is obviously a very important person in our department. And he speaks a lot about his experience and what he does working in system administration. So take a look at that video, you'll be able to watch it, I'll have some questions that will have you answer. And then you'll also have an opportunity to ask a few questions for Seth, I have gone back and talked to all of our speakers from previous semesters, and they have agreed to come in and answer some more questions. So I will make sure that that gets taken care of. 

So this next lab, you're going to basically redo lab one using Puppet, the whole idea behind lab one was to get everybody started with system administration by installing operating systems and VMware and setting everything up. Now we're going to delete all of that. And we're going to do it again. But this time, we're going to use puppet to automate that whole process. So one big important part for lab to make sure you make a snapshot after installing your operating system in puppet so that you have somewhere that you can roll back to. And then throughout the lab, what you're going to do is work on your puppet manifest file tested, see what it does and enroll back to that snapshot, make sure you save your puppet manifest file changes outside of the VM, because when you roll back to that snapshot, it will delete that file. So make sure you save that elsewhere and keep that outside of the VM. So you've got it. 

One big thing is try and keep it simple. Do not try and make this overly complicated. A good solution for this is about 200 lines of code. So it doesn't have to be that big. One thing you can do is use the puppet resource command that I show in several of the videos to query the system. So you can set the system up manually the way you want it. Use puppet resource to see what that looks like as puppet. And then you can copy paste a little bit so that that you need to actually regenerate it into your puppet manifest. That's really all I've got for this week. 

Other than that, feel free to keep in touch by discussing things on Discord or scheduling one on one office hours with me. I'm always happy to chat. If you get stuck on this lab, you can ask me any questions. But other than that, hopefully you're feeling like oh, I have to do this. Again. That's part of the point of system administration is figuring out how we can take something that we do manually and then automate that so that we can do it in a very dependable and reliable way so that all of those computers are going to be set up the exact same way. Best of luck on lab two. Let me know if you have any questions and I look forward to seeing you again in a couple of weeks.

