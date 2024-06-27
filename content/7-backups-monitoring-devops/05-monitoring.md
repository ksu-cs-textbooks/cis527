---
title: "Monitoring"
weight: 25
pre: "5. "
---

{{< youtube Kib5wu3sz1Y >}}

#### Resources

* **[Slides]({{% relref "/7-backups-monitoring-devops/05-monitoring-slides.md"  %}})**
* [Best System Monitoring Tools for Windows & Linux (Free & Paid)](https://www.comparitech.com/net-admin/system-monitoring-tools/) from Comparitech
* [Beocat System Monitor](http://ganglia.beocat.ksu.edu)

#### Video Transcript

One major part of any system administrator's job is to monitor the systems within an organization. However, for many groups, monitoring is sometimes seen as an afterthought, since it requires additional time and effort to properly set up and configure a monitoring system. However, there are a few good reasons to consider investing some time and effort into a proper monitoring system.

First and foremost, proper monitoring will help you keep your systems up and running by alerting you to errors as soon as they occur. In many organizations, systems are in use around the clock, but often IT staff are only available during the working day. So, if an error occurs after hours, it might take quite a while for the correct person to be contacted. A monitoring system, however, can contact that person directly as soon as an error is detected. In addition, it will allow you to more quickly respond to emergencies and cyber threats against your organization by detecting them and acting upon them quickly. Finally, a proper monitoring system can even save money in the long run, as it can help prevent or mitigate large system crashes and downtime.

When monitoring your systems, there are a number of different metrics you may be interested in. First, you'll want to be able to assess the health of the system, so knowing such things as the CPU, memory, disk, and network usage are key. In addition, you might want to know what software is installed, and have access to the log files for any services running on the system. Finally, many organizations use a monitoring system to help track and maintain inventory, as systems frequently move around an organization.

However, beyond just looking at individual systems themselves, you may want to add additional monitoring to other layers of your infrastructure, such as network devices. You may also be involved in monitoring physical aspects of your environment, such as temperature, humidity, and even vibrations, as well as the data from security cameras and monitors throughout the area. In addition, many organizations set up external alerts, using tools such as Google Analytics to be alerted when their organization is in the news or search traffic suddenly spikes. Finally, there are many tools available to help aggregate these various monitoring systems together into a single, cohesive dashboard, and allow system administrators to set customized alert scenarios.

One great example of a system monitoring system is the one from K-State's own Beocat supercomputer, which is linked in the resources section below this video. They use a frontend powered by Ganglia to provide a dashboard view of over 400 unique systems. I encourage you to check it out and see how much interesting data they are able to collect.

Of course, there are many paid tools for this task as well. This is a screenshot of GFI LanGuard, one of many tools available to perform system monitoring and more. Depending on your organization's needs, you may end up reviewing a number of tools such as this for your use.

In the next few videos, I'll discuss some monitoring tools for both Windows and Linux. As part of your lab assignment, you'll install a monitoring system on your cloud servers running on DigitalOcean, giving you some insight into their performance.
