---
title: "Ubuntu Processes & Services"
weight: 80
pre: "16. "
---

{{< youtube mzlFpAfytBE >}}

#### Resources

* **[Slides]({{% relref "/1-secure-workstations/16-ubuntu-processes-services-slides.md"  %}})**
* [How to Use ps, kill, and nice to Manage Processes in Linux](https://www.digitalocean.com/community/tutorials/how-to-use-ps-kill-and-nice-to-manage-processes-in-linux) from DigitalOcean
* [Daemon (Computing)](https://en.wikipedia.org/wiki/Daemon_(computing)) from Wikipedia
* [How to Manage systemd Services on a Linux System](https://www.howtogeek.com/216454/how-to-manage-systemd-services-on-a-linux-system/) from How-To Geek
* [Systemd for Upstart Users](https://wiki.ubuntu.com/SystemdForUpstartUsers) from Ubuntu

#### Video Script

In this video we'll be looking at managing the processes and services running on an Ubuntu Linux system. First, let's take a look at processes. Recall from the earlier video on Windows Processes and Services that a process is a program running in the foreground for the user, while a service is a program running in the background for the operating system.

On Ubuntu, you can see all the running processes using the System Monitor program. It can be found by searching for it after clicking the Activities button. Here you can find information on all running processes, system resources, and file systems. By right-clicking any of the running processes, you'll be given options to view information about the process, or even stop or kill the process if it isn't working properly.

There are also several command-line tools you can use to view the running processes. Installed by default is a program called `top` which will show much of the same information as the System Monitor. Using the keyboard, you can interface with this menu and view more information as well. Press the <kbd>q</kbd> key to quit. There is also a newer, more user-friendly version of top called `htop` but it is not installed by default.

You can also see the running processes by using the `ps` command. By default, it will only show the processes running in that terminal window, so you must use the `-A` option to see all processes on the system. You can also use the `-u` option, followed by a username, to see all the running processes associated with that user, which is very handy on multi-user systems. The `pstree` command works similar, but it shows a tree structure demonstrating which processes were spawned from other processes, which can be very helpful in some instances.

To stop a process via the Terminal, use the `kill` command. Technically, the `kill` command is used to send signals to a process, and it has other uses than just stopping a process, but that is the typical usage. Refer to the documentation linked in the resources section for specific instructions on how to use each of these commands in more detail.

Finally, there are a couple of other system management tools I've found useful over the years. Once of them is `glances`, which is a Python based system monitor that goes well beyond the tools we've seen so far. You can easily install it on your system and get a view like this that shows lots of information about the system. However, since it is based in Python, it installs many additional resources on your system to reach full functionality, which may or may not be desired.

The other tool I recommend is called `saidar`. It is a more traditional terminal program with fewer dependencies, but still gives a good overview of the system. However, it does not display information about individual processes, so it may be of less use in this situation than the others.

Next, let's talk a little bit about services on Linux. In many books and online, you'll see the term daemons used to describe Linux services. That is the more traditional term for these processes that run in the background, and it is still used today by many resources. The term daemon comes from Greek mythology, referring to a being who works tirelessly in the background. It is also a reference to Maxwell's Demon, a similar concept from a well-known thought exercise in physics. Most daemons in Linux today use a process name ending in d, such as `httpd` for a web server or `sshd` for a secure shell server.

On a modern Ubuntu system, the services or daemons are managed by a tool called systemd. Formerly, tools such as init or Upstart were used, but most of them have been phased out at this point in favor of systemd. It is still a very contentious point among Linux enthusiasts, and you'll find lots of discussion online covering the pros and cons of a particular system. I won't go too deep into it here, but if you find references to either init or Upstart online, that's what the discussion is about. To interact with systemd, you can use the `systemctl` command.

For example, to start a service, you would use `sudo systemctl start` followed by the name of the service. Other options such as `stop`, `restart`, and `status` are available. Unfortunately, advanced configuration of systemd services in Ubuntu is a bit outside of the scope of this course, as it is a very involved topic. I encourage you to review the documentation for systemd if you find yourself needing to make any changes to services on your system.
