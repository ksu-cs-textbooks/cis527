---
title: "Windows 10 Overview & Installation"
weight: 25
pre: "5. "
---

TODO

{{< youtube 61zhxNooX-4 >}}

#### Resources

* **[Slides]({{< relref "/1-secure-workstations/05-windows-overview-installation-slides.md" >}})**
* [How to Get Windows 10](https://support.cs.ksu.edu/CISDocs/wiki/FAQ#MSDNAA) from Microsoft Azure Portal via CS Support
* [How to Install VMware Tools](https://kb.vmware.com/s/article/1014294) from VMware
* [Windows 10 Overview](https://www.microsoft.com/en-us/windows/features) from Microsoft
* [Microsoft Windows Version History](https://en.wikipedia.org/wiki/Microsoft_Windows_version_history) from Wikipedia
* [Windows 10 for Windows 7 Users](https://www.howtogeek.com/219034/here%E2%80%99s-what%E2%80%99s-different-about-windows-10-for-windows-7-users/) from How-To Geek
* [Windows 10 for Windows 8 Users](https://www.howtogeek.com/219098/heres-whats-different-about-windows-10-for-windows-8-users/) from How-To Geek
* [Windows 10 Help](https://support.microsoft.com/en-us/products/windows?os=windows-10) from Microsoft
* [Windows 10 Wiki](https://social.technet.microsoft.com/wiki/contents/articles/31032.windows-10-portal.aspx) from Microsoft TechNet
* [Windows 10 Architecture](https://social.technet.microsoft.com/wiki/contents/articles/31048.architecture-of-windows-10.aspx) from Microsoft TechNet
* [Windows 10 ISO Downloads](https://www.microsoft.com/en-us/software-download/windows10) from Microsoft
  - _Warning: May not work with keys from the Microsoft Imagine store! Use the downloads from the store instead._
* [Operating System Market Share](https://netmarketshare.com/operating-system-market-share.aspx?options=%7B%22filter%22%3A%7B%22%24and%22%3A%5B%7B%22deviceType%22%3A%7B%22%24in%22%3A%5B%22Desktop%2Flaptop%22%5D%7D%7D%5D%7D%2C%22dateLabel%22%3A%22Trend%22%2C%22attributes%22%3A%22share%22%2C%22group%22%3A%22platform%22%2C%22sort%22%3A%7B%22share%22%3A-1%7D%2C%22id%22%3A%22platformsDesktop%22%2C%22dateInterval%22%3A%22Monthly%22%2C%22dateStart%22%3A%222017-08%22%2C%22dateEnd%22%3A%222018-07%22%2C%22segments%22%3A%22-1000%22%7D) from Net Market Share
* [How to Add Fast Forward Effect | Davinci Resolve 14 Tutorial](https://www.youtube.com/watch?v=pbiIf44yUMo) from Chris' Tutorials on YouTube

#### Video Script

This video introduces the Windows 10 operating system, and shows how to install it in a virtual machine.

The Windows family of operating systems has the largest market share of all desktop and laptop operating systems, with an estimated 88% of all personal computer systems using some form of Windows. Unsurprisingly, Windows 10 currently holds the largest market share overall, but there are still a large number of systems using Windows 7. Of those, most are either in enterprise organizations who have chosen not to upgrade or owned by home users who rarely purchase a new computer. 

The Windows operating system has a long history. It originally was developed as a graphical "shell" for the MS-DOS operating system, which was popular in the early 1980s. Windows 1.0 was released in 1985, followed by Windows 2.0 and 3.0.

Windows surged in popularity with the release of Windows 95, with 40 million copies sold during its first year. Many features of the modern Windows operating system were present even in Windows 95, such as the control panel, registry, and Internet Explorer web browser.

At the same time, development began on a version of Windows that was not dependent on an underlying DOS-based operating system. This process led to the release of Windows NT, followed by Windows 2000 and Windows XP. Windows XP was the dominant operating system on the market for nearly a decade until it was surpassed by Windows 7, which has been on top ever since.

Windows 10 was released in 2015, and is the most current version of Windows. We'll be using Windows 10 throughout much of this course.

Here is a diagram showing the various versions of Windows and how they relate to one another. Notice that there are a few major families - the DOS versions at the top in red, starting with 1.0. The NT family near the bottom in blue, beginning with NT 3.1, as well as the server versions starting with Server 2003 in green. Finally, in the middle, there are a few mobile versions of Windows as well in yellow and orange, but they have been discontinued in recent years.

Next, let's see how to install Windows 10 in a virtual machine. At this point, I'm assuming you have already installed VMware Workstation or another virtualization software on your computer. If not, I recommend doing so before continuing.

First, you'll need to download the Windows 10 installation file and obtain a product key. Both of those can be found on the Microsoft Azure student portal, which is linked in the resources section below the video. This site now uses your K-State eID and password, making it even easier to access.

Once you log in, simply click Software on the left and search for Windows 10. In the list, find the entry for `Windows 10 (consumer editions), version 1903 - DVD` and download it. On the download page, you can also click this button to access your product key, which you'll need to provide when you install it. 

After you have completed that task, you should have a large installation file in the .ISO file format and a 25 character product key available. You'll need both when installing Windows.

Next, let's open VMware Workstation and create a new virtual machine. For this course, I recommend choosing "I will install the operating system later" to bypass the Easy Install feature of VMware. This will allow you to directly observe the installation process as it would be performed on a real computer.

Next, we will select the type and version of the guest operating system. In this case, it will be Windows 10 x64. We can then give it a helpful name, and choose where it is stored on the computer. If you'd like to store it on a secondary hard disk, you can do so here. I recommend storing your virtual machines on the largest, fastest storage device you have available, preferably an SSD with at least 60 GB of free space.

On the following pages, you can choose the desired disk size and format. You should consult the Lab 1 assignment materials to make sure you choose the correct options here.

Finally, you can click Finish to create the virtual machine. We'll have to customize the hardware anyway, so we can come back to that once it is finished.

Once your virtual machine is created, you can click on the edit virtual machine settings button to customize the hardware. Again, make sure the hardware specification matches what is defined in the assignment for Lab 1. To install the operating system, we'll have to tell the virtual machine where to find the .ISO file downloaded earlier. Click the CD/DVD option, then select the file and make sure it is enabled.

In addition, we'll disable the network during installation so that we'll be prompted to create a local account. Once we are done installing Windows 10, we can re-enable this option to connect to the internet and download updates. 

When you are ready to begin the installation process, click the button to power on the virtual machine. When it powers on, you may be prompted to press any key to install Windows. You'll need to click somewhere inside of the VMWare window before pressing any key in order for the VM to recognize it.

Once it boots, you'll be given the option to install Windows 10. Follow the prompts to install Windows 10 using the Lab 1 assignment as needed for configuration information. The virtual machine may reboot several times during the process.

While installing, you may have to select options to confirm that you don't have access to the internet, and would like to continue with limited setup. This is fine - Windows just _really_ wants us to use a Microsoft account. You may also have to answer some security question - feel free to just make up answers if you want! They won't be needed. 

You can also disable many of the optional features, such as the digital assistant, location data, and targeted advertising. While they are helpful on personal computers, they won't be used in this course. 

When you have successfully installed Windows 10, you'll be ready to move on to configuring Windows 10. The next several videos will discuss that process.

However, before going too far, I recommend installing VMware Tools in the Windows 10 virtual machine. This will allow you to have better control over the virtual machine. You can find instructions for doing that in the resources section below the video.
