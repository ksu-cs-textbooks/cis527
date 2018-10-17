---
title: "Windows Monitoring"
weight: 30
pre: "6. "
---

{{< youtube  >}}

#### Resources

* [Sysinternals Suite](https://docs.microsoft.com/en-us/sysinternals/) from Microsoft
* [11 Useful Tools for Windows SysAdmins](https://anturis.com/blog/11-useful-tools-for-windows-sysadmins/) from Anturis Blog
* [Best System Monitoring Tools for Windows & Linux (Free & Paid)](https://www.comparitech.com/net-admin/system-monitoring-tools/) from Comparitech
* [20 Top Windows SysAdmin Tools You Should Know](https://www.poweradmin.com/blog/top-20-windows-tools-every-sysadmin-should-know/) from Power Admin
* [The Top 20 Free Network Monitoring and Analysis Tools for SysAdmins](https://techtalk.gfi.com/the-top-20-free-network-monitoring-and-analysis-tools-for-sys-admins/) from GFI Tech Talk
* [Top System Monitoring Tools for Windows Environments](https://www.pcwdld.com/best-system-monitoring-tools-for-windows) from PCWDLD

#### Video Transcript

In this video, I'm going to review some of the tools you can use to help monitor the health and performance of your Windows systems. While some of these tools support collecting data remotely, most of them are designed for use directly on the systems themselves. There are many paid products that support remote data collection, as well as a few free ones as well. However, since each one is unique, I won't be covering them directly here. If you'd like to use such a system, I encourage you to review the options available and choose the best one for your environment.

First, of course, is the built-in Windows Task Manager. You can easily access it by right-clicking on the taskbar and choosing it from the menu, or, as always, by pressing <kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>DELETE</kbd>. When you first open the Task Manager on a system, you may have to click a button to show the more details. The Task Manager gives a very concise overview of your system, listing all of the running processes, providing graphs of system performance and resource usage, showing system services and startup tasks, and even displaying all users currently logged-in to the system. It serves as a great first tool to give you some quick insight into how your system is running and if there are any major issues.

From the Performance tab of the Task Manager, you can access the Resource Monitor. This tool gives more in-depth details about a system's resources, showing the CPU, memory, disk, and network usage graphs, as well as which processes are using those resources. Combined with the Task Manager, this tool will help you discover any processes that are consuming a large amount of system resources, helping you diagnose performance issues quickly.

The Windows Performance Monitor, which can be found by searching for it via the Start Menu, also gives access to much of the same information as the Resource Monitor. It also includes the ability to produce graphs, log files, and remotely diagnose another computer. While I've found that it isn't quite as useful as the Resource Monitor, it is yet another tool that could be used to help diagnose performance issues.

Finally, the Windows Reliability Monitor, found on the Control Panel as well as via the Start Menu, provides a combined look at a variety of data sources from your system. Each day, it rates your system's reliability on a scale of 1 to 10, and gives you a quick look at pertinent log entries related to the most recent issues on your system. This is a quick way to correlate related log entries together and possibly determine the source of any system reliability issues.

The Sysinternals Suite of tools available from Microsoft also includes several useful tools for diagnosing and repairing system issues. While I encourage you to become familiar with the entire suite of tools, there are four tools in particular I'd like to review here.

First is Process Explorer. It displays information about running processes on your system, much like the Task Manager. However, it provides much more information about each process, including the threads, TCP ports, and more. Also, Process Explorer includes an option to replace Task Manager with itself, giving you quick and easy access to this tool.

Next is Process Monitor. We've already discussed this tool way back in Module 1. It gives you a deep view into everything your Windows operating system is doing, from opening files to editing individual registry keys. To my knowledge, no other tool gives you as much information about what your system is doing, and by poring over the logged information in Process Monitor, you can discover exactly what a process is doing when it causes issues on your system.

Another tool we've already discussed is TCPView, which allows you to view all TCP ports open on your system, as well as any connected sockets representing ongoing network connections on your system. If a program is trying to access the network, this tool is one that will help you figure out what is actually happening.

Lastly, Sysinternals includes a tool called Autoruns, which allows you to view all of the programs and scripts that run each time your system is started. This includes startup programs in the Start Menu, as well as programs hidden in the depths of the Windows Registry. I've found this tool to be particularly helpful when a pesky program keeps starting with your system, or if a malicious program constantly tries to reinstall itself because another hidden program is watching it.

Windows also maintains a set of log files that keep track of system events and issues, which you can easily review as part of your monitoring routine. The Windows logs can be found by right-clicking on the Start Button, selecting **Computer Management**, then expanding the **Event Viewer** entry in the left-hand menu, and finally selecting the Windows Logs option there. Unlike log files in Ubuntu, which are primarily text-based, the Windows log files are presented in a much more advanced format here. There are a few logs available here, and they give quite a bit of useful information about your system. If you are fighting a particularly difficult issue with Windows, the log files might contain useful information to help you diagnose the problem. In addition, there are several tools available to export these log files as text, XML, or even import them into an external system.

Finally, you can also install Wireshark on Windows to capture network packets, just as we did on Ubuntu in Module 3. Wireshark is a very powerful cross-platform tool for diagnosing issues on your network.

This is just a quick overview of the wide array of tools that are available on Windows to monitor the health and performance of your system. Hopefully you'll find some of them useful to you as you continue to work with Windows systems, and I encourage you to search online for even more tools that you can use in your work.
