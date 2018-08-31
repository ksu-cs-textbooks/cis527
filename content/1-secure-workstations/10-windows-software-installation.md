---
title: "Windows 10 Software Installation"
weight: 50
pre: "10. "
---

{{< youtube ncbKH0-RGfc >}}

#### Resources

* [Slides]({{< relref "/1-secure-workstations/10-windows-software-installation-slides.md" >}})
* [Installation (Computer Programs)](https://en.wikipedia.org/wiki/Installation_(computer_programs)) on Wikipedia
* [Here's What Happens when you Install the Top 10 Download.com Apps](https://www.howtogeek.com/198622/heres-what-happens-when-you-install-the-top-10-download.com-apps/) from How-To Geek
* [Process Monitor](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon) from Microsoft Sysinternals
* [InstallWatch Pro](https://installwatch-pro.en.lo4d.com/) from Lo4d.com

#### Video Script

One major part of configuring a computer is installing the desired software. However, it is sometimes very difficult to tell exactly what is happening during a software installation, and each time you install software on a system you run the risk of introducing more vulnerabilities and stability issues on the system. In this video, I'll give a brief overview of how to observe what is happening when you install a piece of software.

Software on Windows typically consists of several components. First, you have the actual executable itself, as a .EXE file. It may also have several dynamic link libraries, or DLLs, that it uses. A DLL is simply a shared library of code that can be used by other programs or updated without changing the executable file itself. There could also be settings files such as initialization files, or settings stored as registry keys in the Windows registry. Finally, depending on the software it may also install drivers or services as well. Let's look at one piece of software that is pretty common and see what it does when we install it on our system.

On this system, I have installed InstallWatch Pro, which is available in the Resources section below the video. I've also downloaded a copy of Process Monitor from the Microsoft Sysinternals suite of tools. Finally, I downloaded a full installer for Mozilla Firefox.

First off, I need to start InstallWatch Pro and let it make a snapshot of the current system. This process may take several minutes.

Once that is done, I can also start Process Monitor. It will start recording data automatically.

Then, I can instruct InstallWatch Pro to install Mozilla Firefox by providing the location of the installation file here.

When the installation process starts, I'll just click the default options in the installer and let it continue as it would normally.

When it is finished, InstallWatch Pro will pop back up, and you'll need to click Finish there so it can work on making a new snapshot after the installation. You should also quickly go to Process Monitor, then click File and uncheck the Capture Events option.

Once InstallWatch Pro is done making a new snapshot, it will display all of the items installed by Mozilla Firefox. We can see several files were added, mostly in the Program Files folder. There were also many keys added to the registry. I recommend doing this process on your own virtual machine at least once and reviewing what you find.

In Process Monitor, we can add a filter to just see all items performed by the Mozilla Firefox setup process, which uses "setup.exe" as its process name. Just click the filter button at the top, and add the appropriate filter. Now we can see each and every option performed by the setup process. In this case, there are nearly 100,000 of them! It could be very tedious to dig through, but if you know you are looking for a particular item, you can use the search features in Process Monitor to find it very quickly.

As you continue working on Lab 1, I encourage you to take a little time and see what each program installs. You might be surprised!
