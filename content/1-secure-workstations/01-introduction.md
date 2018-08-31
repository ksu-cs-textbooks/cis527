---
title: "Introduction"
weight: 5
pre: "1. "
---

{{< youtube Zd1M6KhQ-6M >}}

#### Resources

* [Slides]({{< relref "/1-secure-workstations/01-introduction-slides.md" >}})
* [Operating System](https://en.wikipedia.org/wiki/Operating_system) on Wikipedia
* [Types of Operating Systems](https://www.geeksforgeeks.org/operating-system-types-operating-systems-awaiting-author/) on Geeks for Geeks
* [Understanding Operating Systems](https://edu.gcfglobal.org/en/computerbasics/understanding-operating-systems/1/) on GCF LearnFree
* [GNU/Linux Naming Controversy](https://en.wikipedia.org/wiki/GNU/Linux_naming_controversy) on Wikipedia
* [The Great Debate: Is it Linux or GNU/Linux?](https://www.howtogeek.com/139287/the-great-debate-is-it-linux-or-gnulinux/) on How-To Geek

#### Video Script

Welcome to the first module in this class! Module 1 is all about creating secure workstations. In this module, you'll learn how to install virtual machine software, install the operating systems we'll be using in the class, and then configure several aspects of the operating systems. You'll create users, manage file permissions, install software, and secure those systems.

Before we begin, here is a short overview of one major concept in this module - the operating system. Every computer you use has some sort of operating system installed, even if you don't realize it. For this module, we'll be using the two most commonly used operating systems in industry today, Microsoft Windows 10 and Ubuntu Linux. I'm guessing that most of you have used at least one of these systems before, and in fact many of you are probably using one of them now.

Operating systems make up the core of a modern computer. This diagram shows exactly where the operating system fits in a larger hierarchy. A computer consists of hardware, and the operating system is the program that runs directly on the hardware. It is responsible for interfacing with the hardware, and running the applications needed by the user. On the very first computers, each application was itself an operating system. This allowed the programs to directly interface with the hardware, but the major drawback was that only one program could run at a time, and the computer had to be restarted between each program. In addition, each program would need to be customized to match the hardware it was running on.

By using an operating system, applications can be much more generalized, and multiple applications can be running at the same time. Meanwhile, hardware can be changed, sometimes even while the computer is running, and the operating system will manage the necessary interfaces to use that hardware. It is a very efficient system.

The major part of the operating system is called the kernel. It is the part specifically responsible for creating the interface between user applications and the hardware on the system. In fact, most of what you may consider an operating system is in fact applications running on the kernel. The start menu, control panel, and registry are actually applications in Windows. Because of this, there is some disagreement over whether they are considered part of the operating system or not. The same discussion has been going on for years in the Linux community. See the resources section for links to the discussion of GNU vs. Linux.

For this course, anything referring to the kernel or programs typically bundled along with the kernel will be considered the operating system. This follows the typical convention in most system administrator resources online.

If you are interested in learning about how operating system are built and how the kernel functions, consider taking CIS 520: Operating Systems.

Next, we'll start discussing Windows 10 and Ubuntu Linux in detail.
