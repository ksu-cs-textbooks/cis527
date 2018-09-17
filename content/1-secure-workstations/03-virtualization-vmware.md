---
title: "Virtualization & VMware"
weight: 15
pre: "3. "
---

{{< youtube dkVgU6twaXM >}}

#### Resources

* **[Slides]({{< relref "/1-secure-workstations/03-virtualization-vmware-slides.md" >}})**
* [Virtualization](https://en.wikipedia.org/wiki/Virtualization) on Wikipedia
* [Virtualization Whitepaper](https://www.vmware.com/pdf/virtualization.pdf) from VMware
* [Accessing VMware Software](https://support.cs.ksu.edu/CISDocs/wiki/FAQ#VMWare) on CS Support

#### Video Script

In this class, we will be making heavy use of virtualization software to allow us to run multiple operating systems simultaneously on the same computer. This video provides a quick overview of what virtualization is and how it works.

First, a simple view of how a computer works. In essence, whenever you tell the computer to run a program, you are actually telling the operating system what to do. It will then load the requested application software into memory, and begin executing it. The software will send instructions through the operating system to the hardware, describing what actions to take. The hardware will then use electronic circuits to perform those operations.

This diagram shows that a computer would look like without virtualization. This describes how most computers work today, and it has been this way for over 30 years.

Recently, however, virtualization has become much more commonplace. In fact, you may be using some forms of virtualization right now, and not even realize it. In essence, virtualization software emulates some part of a computer system, typically the hardware. By doing so, it allows the hardware to run multiple different operating systems at the same time. Also, it prevents the different operating systems from conflicting with each other.

As an added bonus, by using virtualization, it becomes much easier to migrate operating systems across different hardware setups. Instead of having to reinstall and reconfigure the operating system on the new hardware, simply install the virtualization platform, and copy the virtual machine as if it were any other file.

In essence, virtualization adds one more layer of abstraction between the kernel and the hardware, allowing it to be much more portable and configurable than in a traditional setup. This diagram gives an overview of what that would look like.

Of course, there are many different types of virtualization out there. In this class, we'll be primarily working with hosted virtualization, which involves installing virtualization software within a "host" operating system. You can also install virtualization software directly on the hardware, which is called bare-metal or hypervisor virtualization.

Beyond that, you can choose to virtualize more than just the hardware. Parts of the operating system itself can be virtualized, leading to the concept of containers, such as those employed by Docker. You can also virtualize parts of individual applications to make them more secure. This is commonly called sandboxing, and many mobile operating systems and browsers today already employ sandboxing between the apps and pages they work with.

This diagram shows what hosted virtualization looks like. You'll notice that there is a host operating system installed on the hardware itself, and the virtualization layer is installed on top of that.

Compare that to bare-metal virtualization, where the virtualization layer is installed directly on top of the hardware. This is especially powerful, since the system doesn't have to devote any resources to running the host operating system if it won't be directly used.

This diagram gives a good overview of containers. In this case, the docker engine acts as the virtualization layer. Inside the containers, instead of having a full operating system, you simply have libraries and applications. They all share the same kernel, provided by the host operating system, though they can have different configurations within each container. It is a very powerful way to deploy applications on cloud servers.

Finally, this diagram gives a quick look at sandboxing. By virtualizing the parts of the system that an application interacts with, you can prevent it from performing malicious actions and interfering with other parts of the system.

To quote Men in Black, the "old & busted" way of doing things involved installing a single operating system per server, and then a single application on that server. This resulted in organizations managing large numbers of physical servers. In addition, most servers were only running at 5% capacity, so the resources were very inefficiently used. Finally, it was a management nightmare, and the only way to add more redundancy to the system was to buy more servers, compounding the problem.

Compare that to the "new hotness" of today, where we can use virtualization to install many operating systems on a single physical server, with each one dedicated to a single application. That results in fewer physical servers, more efficient use of resources, and much simpler redundancy. However, it is up for debate if that truly made management easier, or if it just shifted the management chore from installing and configuring individual systems to installing and configuring deployment and automation tools.

For this course, we'll be primarily working with hosted virtualization using VMware Workstation. If you are using an Apple computer, you'll be using VMware Fusion, which is very similar. I highly recommend using this software, as all of the materials in this class have been tested on it, and I am very familiar with it in case you need help. It is available to all K-State CS students for free. A link to the instructions for finding that software is in the resources section below.

However, you may choose to use a different virtualization software package to meet your needs. The only thing to keep in mind is that I can make no guarantees that it will work, and if you run into major issues that we cannot fix, you may be asked to continue working on the labs in this class using VMware products instead. Here is a list of a few other software packages that could be used instead of VMware Workstation or fusion.

Again, if you do not have access to a computer with sufficient resources to install and use VMware, please contact me so we can make other arrangements.

Finally, beyond just virtualization software, there are many cloud providers that will host virtual machines for you. We'll deal with these more starting in module 5. This list gives a few of the more popular ones out there.

In addition, many cloud providers offer more than just virtual machines, such as containers and application hosting. Again, we'll discuss these more starting in module 5, but here are a few you may have heard of.

At this point, you should be ready to complete the first task of Lab 1, which is to install Virtualization Software. Make sure you install the proper version, as listed on the Lab 1 Assignment page. If you have any questions, please use the discussion boards to ask your fellow classmates or contact me.
