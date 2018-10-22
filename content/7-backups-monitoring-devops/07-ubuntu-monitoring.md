---
title: "Ubuntu Monitoring"
weight: 35
pre: "7. "
---

{{< youtube _1t4rTbwEFE >}}

#### Resources

* [20 Command Line Tools to Monitor Linux Performance](https://www.tecmint.com/command-line-tools-to-monitor-linux-performance/) from TecMint
* [80 Linux Monitoring Tools](https://blog.serverdensity.com/80-linux-monitoring-tools-know/) from Server Density Blog
* [System Monitoring Tools for Ubuntu](https://askubuntu.com/questions/293426/system-monitoring-tools-for-ubuntu) from AskUbuntu
* [Best System Monitoring Tools for Windows & Linux (Free & Paid)](https://www.comparitech.com/net-admin/system-monitoring-tools/) from Comparitech
* [The Top 20 Free Network Monitoring and Analysis Tools for SysAdmins](https://techtalk.gfi.com/the-top-20-free-network-monitoring-and-analysis-tools-for-sys-admins/) from GFI Tech Talk
* [Seamless Infrastructure Monitoring](https://www.digitalocean.com/products/monitoring/) from DigitalOcean
* [Monitoring Quickstart](https://www.digitalocean.com/docs/monitoring/quickstart/) from DigitalOcean
* [How to Set Up Monitoring Alerts](https://www.digitalocean.com/docs/monitoring/how-to/set-up-alerts/) from DigitalOcean

#### Video Transcript

Ubuntu also has many useful tools for monitoring system resources, performance, and health. In this video, I'll cover some of the more commonly used ones.

First and foremost is the System Monitor application. It can easily be found by searching for it on the Activities menu. Similar to the Task Manager on Windows, the System Monitor allows you to view information about all the running processes, system resources, and file systems on Ubuntu. It is a very useful tool for discovering performance issues on your system.

Of course, on Ubuntu there is an entire universe of command-line tools that can be used to monitor the system as well. Let's take a look at a few of them.

First is `top`. Similar to the System Monitor, `top` allows you to see all running processes, and it sorts them to show the processes consuming the most CPU resources first. There are commands you can use to change the information displayed as well. In addition, you may also want to check out the `htop` command for a more advanced view into the same data, but `htop` is not installed on Ubuntu by default.

In addition to `top`, you may also want to install two similar commands, `iotop` and `iftop`. As you might expect, `iotop` shows you all processes that are using IO resources, such as the file systems, and `iftop` lists the processes that are using network bandwidth. Both of these can help you figure out what a process is doing on your system and diagnose any misbehavior.

To view information about memory resources, you can use either the `vmstat` or `free` commands. The `free` command will show you how much memory is used, and `vmstat` will show you some additional input and output statistics as well.

Another command you may want to install is `iostat`, which is part of the `sysstat` package. This command will show you the current input and output information for your disk drives on your system.

In addition, you can use the `lsof` command to see which files on the system are open, and which running process is using them. This is a great tool if you'd like to figure out where a particular file is being used. I highly recommend using the `grep` tool to help you filter this list to find exactly what you are looking for.

In Module 3, we discussed a few network troubleshooting tools, such as the `ip` and `ss` commands, and Wireshark for packet sniffing. So, as you are working on monitoring your system, remember that you can always use those as well.

Finally, you can also use the `watch` command on Ubuntu to continuously run a command over and over again. For example, I could use `watch tail /var/log/syslog` to print the last few lines of the system log, and have that display updated every two seconds. This command is very handy when you need to keep an eye on log files or other commands as you diagnose issues. If you are running a web server, you may also want to keep an eye on your Apache access and error logs in the same manner.

There are also a few programs for Ubuntu that integrate several different commands into a single dashboard, which can be a very useful way to monitor your system. The two that I recommend using are `glances` and `saidar`. Both can easily be installed using the APT tool. Glances is a Python-based tool that reads many different statistics about your system and presents them all in a single, unified view. I especially like running it on systems that are not virtualized, as it can report information from the temperature sensors built-in to many system components as well. It even has some built-in alerts to help you notice system issues quickly. Saidar is very similar, but shows a slightly different set of statistics about your system. I tend to use both on my systems, but generally I will go to Glances first.

As I mentioned a bit earlier, Ubuntu stores a plethora of information in log files stored on the system. You can find most of your system's log files in the `/var/log` directory. Some of the more important files there are `auth.log` which tracks user authentications and failures, `kern.log` which reports any issues directly from the Linux kernel, and `syslog` which serves as the generic system log for all sorts of issues. Some programs, such as Samba and Apache, may create their own log files or directories here, so you may want to check those as well, depending on what your needs are. As with Windows, there are many programs that can collect and organize these log files into a central logging system, giving you a very powerful look at your entire infrastructure.

Lastly, if you are running systems in the cloud, many times your cloud provider may also provide monitoring tools for your use. DigitalOcean recently added free monitoring to all droplets, as long as you enable that feature. You can view the system's monitoring output on our DigitalOcean dashboard under the **Graphs** option. In addition, you can configure alert policies to contact you when certain conditions are met, such as sustained high CPU usage or low disk space. I encourage you to review some of the available options on DigitalOcean, just to get an idea of what is available to you.

That should give you a quick overview of some of the tools available on an Ubuntu system to monitor its health and performance. There are a number of tools available online, both free and paid, that can also perform monitoring tasks, collect that data into a central hub, and alert you to issues across your system. As part of the lab assignment, you'll configure either Munin or Ganglia to discover how those tools work.
