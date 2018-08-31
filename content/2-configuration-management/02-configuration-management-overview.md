---
title: "Configuration Management Overview"
weight: 10
pre: "2. "
---

{{< youtube oCkDAdMDiqw >}}

#### Resources

* [Slides]({{< relref "/2-configuration-management/02-configuration-management-overview-slides.md" >}})
* [Configuration Management](https://en.wikipedia.org/wiki/Configuration_management) on Wikipedia
* Configuration Management(https://puppet.com/solutions/configuration-management) from Puppet
* [Modern Configuration Management: Configuration as Code](https://www.chef.io/configuration-management/) from Chef
* [Use Case: Configuration Management](https://www.ansible.com/use-cases/configuration-management) from Ansible
* [Configuration Management](https://www.mitre.org/publications/systems-engineering-guide/acquisition-systems-engineering/configuration-management) from MITRE Systems Engineering Guide
* [SaltStack Enterprise](https://saltstack.com/saltstack-enterprise/) from SaltStack
* [DevOps](https://en.wikipedia.org/wiki/DevOps) on Wikipedia
* [What Is DevOps?](https://theagileadmin.com/what-is-devops/) From The Agile Admin
* [What is this DevOps Thing, Anyway?](http://www.jedi.be/blog/2010/02/12/what-is-this-devops-thing-anyway/) From Just Enough Developed Infrastructure (JEDI)
* [Periodic Table of DevOps Tools](https://xebialabs.com/periodic-table-of-devops-tools/) from XebiaLabs

#### Video Script

This module deals with the topic of configuration management. Before I introduce that topic directly, let's look at what we've done so far in this class.

In Lab 1, you were asked to set up and configure a single operating system VM for both Windows and Linux. For many system administrators, that is exactly how they operate on real systems - each one is set up by hand, one at a time, manually. This process, of course, does have some benefits. For the sysadmin, they get hands-on management with each computer they support. In addition, they can easily customize each system to meet the individual needs of the user. For sysadmins with a low level of experience, or few resources, this can be a very easy way to at least help users configure their systems. And, in practice, this method works well for small groups of users. If you are only supporting a few users, maybe even up to several dozen, manually managing systems and configurations may be the most efficient and cost-effective way to do so.

However, there are some major downsides to this as well. First and foremost, it is a very time consuming and labor intensive process. You probably experienced that while working on the first lab. Depending on your own experience and familiarity with those systems and the tasks at hand, it may have taken anywhere from one to several hours to complete. While you can, of course, become more proficient, it may still take quite a bit of hands-on time to configure an operating system. In addition, there is the high likelihood of machines being configured inconsistently, leading to additional support headaches down the road. I can confidently say from my time working as a sysadmin and from grading labs in this class, even with the same simple instructions, it is very difficult for any two people to configure a computer in exactly the same way. Also, as new software and operating system updates are released, you'll find that you need to install them on a per-machine basis, or depend on the end users to do those updates themselves. Finally, as your groups get larger, this approach really doesn't scale well at all.

So, that leads to the big question - how do we make this process scalable?

One way to do this is through the use of automation tools, such as GNU Make. While Make was developed to help with compiling large pieces of code, it shares many similarities with the tools we'll look at in this module. Many system administrators also wrote scripts to automate part of their process, but in most cases those scripts were simply a list of steps or commands that the sysadmin would run manually, and they would have to be customized to fit each particular operating system or configuration.

There are also a couple of techniques that can be used to scale this process. One is through the use of system images. Much like the virtual machines we are using in this class, you can actually store the entire hard drive of a computer as a system image and copy it as many times as you'd like to machines. However, this process is also very time-consuming since the images are so big, and they can only be copied onto the same or similar hardware configurations. This is great when everyone has the same hardware, but in many organizations that simply isn't the case. Lastly, you can also use tools to create custom operating system installers for both Windows and Linux, with much of the configuration and software pre-installed and configured along with the operating system. Again, this is very time consuming, and it must be redone and updated every time something changes. In addition, none of these methods really address how to handle updates and new software once the system is in the hands of the users. In short, we need something better.

Enter the concept of a defined configuration. Imagine this: what if we could write out exactly how we would like our computers to be configured, and then direct our staff to make sure the system matched that configuration, regardless of the operating system or hardware? That configuration would be a list of configured items only, not a set of steps to accomplish that task. In essence, much of the first lab assignment could be thought of as a defined configuration. Those items are high level, system independent, and hopefully just enough information that any competent system administrator could build a system that meets those requirements. If that is the case, could we build a software tool to do the same?

This is the big concept behind configuration management. As a system administrator, all you have to do is define your desired configuration in a way that these tools can understand it, then they will do the rest. In that way, you can think of your system configuration as just another piece of "source code" and manage it just like any other code. If you need to deploy a new piece of software or update one, simply change the configuration file and every system using the tool will make the necessary changes to match. By doing so, this will greatly reduce downtime and errors and increase the consistency of all the systems you are managing. According to one estimate, 70% of all downtime in datacenters is due to human error, so the more we can take humans out of the equation, the better.

There are many tools available for configuration management. For this class, we'll be using Puppet as it is one of the easiest tools to work with in my experience, and it is available for a variety of platforms and uses. If you are interested in using configuration management tools in your own work, I encourage you to review each of these platforms, as each one offers unique features and abilities.

As we discuss automation tools, I briefly want to bring up the term DevOps, since it is really one of the big things you'll hear discussed on the internet today. DevOps is a shortened form of "development operations" and is, in essence, a very close collaboration between software development and system administration staff. A good way to think of this is the application of "agile" software development practices to the world of system administration, so that the systems can be as "agile" (pun intended) as the developers want them to be. This involves a high level of automation and monitoring, both in terms of configuration management but also deployment and testing. There are also the very short development cycles traditionally seen in agile development, with increased deployment frequency. We'll spend a little bit of time talking about DevOps later in the course, but many of the concepts we are covering here in configuration management are very applicable there as well.

Finally, here are a few tools from the DevOps world you may come across. Some of the biggest ones, Jenkins and Travis, are used for build and test automation, while tools such as Nagios and Icinga are helpful for system monitoring. Feel free to check out any of these tools on your own time, as you may find several of them very useful.
