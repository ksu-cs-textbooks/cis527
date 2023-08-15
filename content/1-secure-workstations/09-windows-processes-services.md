---
title: "Windows 10 Processes & Services"
weight: 45
pre: "9. "
---

{{< youtube TNRyA5NJNEc >}}

#### Resources

* **[Slides]({{< relref "/1-secure-workstations/09-windows-processes-services-slides.md" >}})**
* [How to manage services in Windows](https://www.digitalcitizen.life/what-are-windows-services-what-they-do-how-manage-them/) from DigitalCitizen.life
* [Process Explorer Download](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer) from Windows Sysinternals
* [Process Library](http://www.processlibrary.com/en/) from Uniblue

#### Video Script

Let's take a look at how Windows interacts with programs. Each program running on an operating system is called a process. Within each process, there can be multiple threads of execution running concurrently. As a system administrator, the most important thing to keep in mind is that each process running on a computer will consume the system's resources, either the available memory or CPU time. So, the more processes you run, the slower your computer may seem as you consume more of the available resources.

The operating system stores a few important pieces of information about each process. The most notable is the PID or process identifier. Much like the user accounts and groups, each running process is given an identifier. In this way, if you have multiple copies of the same program running, each one will have a different PID.

To examine processes on Windows, there are a couple of tools available. First, built-in to Windows is the Task Manager. It has been present in Windows since the early days, and gives lots of information about the processes running on a system. You can access it quickly by right-clicking on an open area of the taskbar, or by using the classic <kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>DEL</kbd> key combination.

Another tool I recommend is Process Explorer, part of the Microsoft Sysinternals suite of tools for Windows. You can download it using the link in the resources below this video. Using Sysinternals, you can see additional details about each process running on a computer. You can also replace the built-in Task Manager with Process Explorer if you so choose.

On Windows, you'll notice that even though we aren't running any programs, there are still dozens of processes running in the background. Most of them are what we call Services. A service is a process that runs in the background on Windows, and is usually started and managed by the operating system. They perform many important tasks, such as maintaining our network connection, providing printing functions, and logging important system events.

To access the services on Windows, simply search for the Services app on the Start Menu. Here you can see all the services installed on your system, as well as their description, status, and more. I'm going to choose one to review in detail.

On the first screen, you'll see some of the general information about the service. It includes the startup type, which could be either automatic, delayed, manual, or disabled. You can also start or stop the service here.

On the Log On tab, you'll see the user account used to run the service. Just like with any other process on Windows, each service must be associated with a user account in order to determine what permissions that process will have. On Windows, there are actually three pseudo accounts that are typically used with services. Those accounts are LocalSystem, LocalService, and NetworkService. Of course, you can always override these defaults and provide the information for another user account, but then this service will have the same permissions as that account.

The Recovery tab describes what actions the system should take if the service fails for any reason. Again, you probably won't need to modify these options unless you are working with services of your own, but it is important to know that they can be configured here. For example, if an important process fails, you could have the computer automatically restart itself or run a program to notify you.

Finally, the Dependencies tab lets you see any other services that this one depends on, or services that depend on this one. Many Windows services require other services to be active before they will work properly.

One important thing to note about Windows services in particular is the use of the Service Host Process, or svchost.exe. To help conserve resources, Windows can actually embed several services as threads in a single process. In that way, the operating system only has to manage a single process instead of several. If you look at the processes running in Task Manager, you'll see several entries for Service Host. You can even click the arrow next to that process to see which services are embedded in it. Unfortunately, because this creates a single point of failure, the Service Host Process is a frequent target of Windows malware and viruses. In fact, I once saw a virus try to hide its own executable by naming it svcnost.exe, hoping that a system administrator wouldn't notice the slight spelling difference very quickly.

With this background information, you are ready for the next step, which is to install some software.
