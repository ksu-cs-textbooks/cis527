---
title: "Puppet Resources"
weight: 25
pre: "5. "
---

{{% notice info "Puppet Learning VM Deprecated" %}}

_As of 2023, the Puppet Learning VM is no longer being maintained. The videos below demonstrate some of the features of Puppet, which can also be done on your Ubuntu VM after installing Puppet Agent. Unfortunately, it is not easily possible to simulate an enterprise Puppet setup without this VM, so I'll keep these videos up for demonstration purposes._ --Russ

{{% /notice %}}

{{< youtube KAnRoCS2NHo >}}

#### Resources

* **[Slides]({{< relref "/2-configuration-management/05-puppet-resources-slides.md" >}})**
* [Core Types Cheat Sheet](https://puppet.com/docs/puppet/latest/cheatsheet_core_types.html) from Puppet
* [Resource Type Reference](https://puppet.com/docs/puppet/latest/type.html) from Puppet

#### Video Script

In this video, we will begin learning how to use Puppet to configure a system. Before creating our own Puppet scripts, called Manifest Files, we will discuss how Puppet actually views a system it is configuring.

In Puppet, a system is simply a set of resources. There are many different types of resources, such as files, user accounts, installed programs, and more. In addition to a type, each resource has a title, and a set of attributes giving additional information about the resource. The resources section below the video has links to the Puppet documentation for resource types.

Let's review some different resources using the Puppet Learning VM. You can also perform many of these same operations on your Windows and Linux computers with Puppet Agent installed. If you'd like to follow along, I'll be working in the `hello_puppet` quest on the Puppet Learning VM.

I have already performed the first task for the `hello_puppet` quest, so I'm now connected to one of the internal systems and installed the Puppet Agent on it. Now, I can start Task 2, where I review a file resource. Using Puppet, you can describe a file resource such as the following:

```bash
sudo puppet resource file /tmp/test
```

That should give you information about that file. Here you can see that the resource is of type file, and has its path for a title. Below that are the attributes of the file, given as `parameter => value` pairs. Since the file doesn't exist, the only attribute visible is the ensure attribute, and it shows that the file is absent on the system.

We can easily create the file using this command:

```bash
touch /tmp/test
```

Then we can use the same resource command to view it:

```bash
sudo puppet resource file /tmp/test
```

Now we can see many additional attributes of the file.

We can also use the `puppet resource` command to modify resource. For example, let's add some content to that file:

```bash
sudo puppet resource file /tmp/test content='Hello Puppet!'
```

Once you run that command, you can view the contents of the file to confirm that it worked:

```bash
cat /tmp/test
```

There are many types of resources that can be viewed and modified in this way. For example, you can view information about a user account, such as the learning account on the current VM:

```bash
sudo puppet resource user learning
```

You can also find information about installed software packages, such as the Apache Webserver `httpd`:

```bash
sudo puppet resource package httpd
```

In this case, since the package is not installed on the system, the ensure attribute is set to purged, which is similar to absent.

The Puppet Learning VM quest describes how to see the inner workings of a Puppet Resource by breaking it. I'm not going to go over that process in detail, but I recommend you review that information on your own.

As with the file, we can configure attributes easily enough:

```bash
sudo puppet resource package httpd ensure=present
```

That command will install the latest version of the `httpd` package. Note that when it executes, the ensure value is changed to the current version. Later, as you define your Puppet manifests, you can use the ensure attribute to install the latest version using the `present` value, or provide a specific version number here if desired.

There are many different types of resources available in Puppet. I encourage you to review some of the documentation linked below this video before continuing, just to get an idea of what is available. The next video will describe how to create your own Puppet Manifest Files and apply them to a system directly using the Puppet Agent.
