---
title: "Ubuntu Overview & Installation"
weight: 60
pre: "12. "
---

{{< youtube MtG2xyyW6dI >}}

<!-- PLn3N9jYp7s -->

#### Resources

* **[Slides]({{% relref "/1-secure-workstations/12-ubuntu-overview-installation-slides.md"  %}})**
* [VMware/Tools](https://help.ubuntu.com/community/VMware/Tools) from Ubuntu
* [Ubuntu Features](https://www.ubuntu.com/desktop/features) from Ubuntu
* [Ubuntu Desktop Guide](https://help.ubuntu.com/lts/ubuntu-help/index.html) from Ubuntu
* [Ubuntu Server Guide](https://help.ubuntu.com/lts/serverguide/index.html) from Ubuntu
* [Switching to Ubuntu](https://help.ubuntu.com/community/SwitchingToUbuntu) from Ubuntu
* [Know Thy Ubuntu](https://help.ubuntu.com/community/KnowThyUbuntu) from Ubuntu
* [Ubuntu 22.04 LTS (Jammy Jellyfish) Download](http://mirror.cis.ksu.edu/ubuntu-releases/jammy/) from CS Ubuntu Mirror
* [Linux Distribution Timeline](https://commons.wikimedia.org/wiki/File:Linux_Distribution_Timeline.svg) from Wikipedia
* [Desmond Tutu on Ubuntu](https://www.youtube.com/watch?v=ftjdDOfTzbk) from YouTube

#### Video Script

For the second part of this module, we'll be looking at one other operating system, Ubuntu.

Ubuntu is built using the Linux kernel, which is a completely free and open source operating system kernel developed by Linus Torvalds in 1991. It was his attempt to make a free operating system kernel which would be completely compatible with the Unix operating system via the POSIX standard. There were some previous attempts to do so, most notably the GNU project from the 1980s.

While Linux is usually thought of as an operating system, in actuality it is best thought of as an operating system kernel. Linux is typically bundled with other software and tools, such as the GNU project, and those bundles are referred to as Linux distributions. There are hundreds of Linux distributions available, each one customized to fit a particular need or design.

Here is a quick family tree for the Linux kernel. You can see that it all started with the Unix operating system developed by Bell Labs in the 1970s. It was forked into the BSD family, which still exists today. The underlying kernel for the Mac OS X operating system, Darwin, is still based on the original BSD family of Unix. In the 1980s, Richard Stallman created the GNU project, with an ultimate goal of creating a free version of Unix that was completely open source. That project stalled, but around the same time Linux was introduced. For most users, the Linux kernel coupled with the GNU tools is typically what they think of when they think of Linux as an operating system.

Linux itself is a very versatile kernel, and is used everywhere from the Android mobile operating system all the way to the world's largest super computers, and nearly everything in between. Basically, if it needs an operating system kernel, there is a good chance that someone has tried to run Linux on it at some point.

For this class, we'll be looking at the Ubuntu software distribution. Ubuntu is a term from the Nguni Bantu language, meaning humanity, and comes from a philosophy of the same name popularized by Nelson Mandela and Desmond Tutu, among others. Ubuntu itself is based on an older Linux distribution called Debian, which is very popular among many server administrators even today. Since its inception, Ubuntu strives for a new release every 6 month, with every 4th release (every 2 years) being listed as a Long Term Support or LTS release, which is supported with software and security updates for 5 years from release. Depending on the metric used, Ubuntu Linux is generally seen as the most common and most popular Linux distribution in the world for desktops and servers.

As a quick aside, here is the current Linux distribution family tree. The full version of it is linked in the resources section below the video. Ubuntu is shown here as a major branch of the Debian family.

The first major release of Ubuntu was known as Ubuntu 4.10 - Warty Warthog. Each Ubuntu release is given a version number based on the month and year of its release, in this case October of 2004, as well as a code name typically consisting of an alliterative adjective and animal combination. The first LTS release was in 2006 as Dapper Drake. Since that time, there have been 7 other LTS releases:

* 8.04 - Hardy Heron
* 10.04 - Lucid Lynx
* 12.04 - Precise Pangolin
* 14.04 - Trusty Tahr
* 16.04 - Xenial Xerus
* 18.04 - Bionic Beaver
* 20.04 - Focal Fossa

The most recent version, Focal Fossa, is the current LTS version and the one we'll be using in this class.

{{% notice note %}}
_Of course, many new Ubuntu versions may have been released since this video was recorded. However, we'll stick with the 20.04 LTS version, Focal Fossa, since it will be maintained for many years. --Russ_
{{% /notice %}}

Now, let's go through the process of installing Ubuntu in a virtual machine. At this point, I'm assuming you have already installed VMware Workstation or another virtualization software on your computer. If not, I recommend doing so before continuing.

First, you'll need to download the Ubuntu 20.04 installation file. You can find that file on the Ubuntu download page, and also on the K-State CS mirror of the Ubuntu downloads page. For most uses, I recommend using the CS mirror, as it is generally much faster for students on campus. The link is available in the Resources section below the video. On that page, you'll need to download the "64-bit PC (AMD64) desktop image" from the link near the top. It should download a file to your computer in the .ISO format.

Next, let's open VMware Workstation and create a new virtual machine. For this course, I recommend choosing "I will install the operating system later" to bypass the Easy Install feature of VMware. This will allow you to directly observe the installation process as it would be performed on a real computer.

Next, we will select the type and version of the guest operating system. In this case, it will be "Ubuntu 64-bit." We can then give it a helpful name, and choose where it is stored on the computer. If you'd like to store it on a secondary hard disk, you can do so here. I recommend storing your virtual machines on the largest, fastest storage device you have available, preferably an SSD with at least 60 GB of free space.

On the following pages, you can choose the desired disk size and format. You should consult the Lab 1 assignment materials to make sure you choose the correct options here.

Finally, you can click Finish to create the virtual machine. We'll have to customize the hardware anyway, so we can come back to that once it is finished.

Once your virtual machine is created, you can click on the edit virtual machine settings button to customize the hardware. Again, make sure the hardware specification matches what is defined in the assignment for Lab 1. To install the operating system, we'll have to tell the virtual machine where to find the .ISO file downloaded earlier. Click the CD/DVD option, then select the file and make sure it is enabled.

When you are ready to begin the installation process, click the button to power on the virtual machine.

Once it boots, you'll be given the option to install Ubuntu. Follow the prompts to install Ubuntu using the Lab 1 assignment as needed for configuration information. In general, you can accept the defaults in the installer unless otherwise noted. For the timezone, you can choose Chicago as the nearest city.

Once the installation is complete, you'll be prompted to reboot your computer. In rare instances, the virtual machine may not reboot correctly. If that happens, you can use the VM menu in VMware to restart the virtual machine. It should not cause any issues as long as the installation process completed.

At this point, you are ready to begin Lab 1, Task 4 - Install Ubuntu 20.04. Feel free to get started!

Once that is complete, you'll be ready to move on to configuring Ubuntu. The next several videos will discuss that process.

However, before going too far, I recommend installing either "open-vm-tools-desktop" or VMware Tools in the Ubuntu virtual machine. This will allow you to have better control over the virtual machine. You can find instructions for doing that in the resources section below the video.

Also, I recommend taking a minute to familiarize yourself with the filesystem structure in Ubuntu. You'll learn more about how to navigate this structure in the following videos. This diagram shows the common root-level folders you'll find and the typical usage of each.
