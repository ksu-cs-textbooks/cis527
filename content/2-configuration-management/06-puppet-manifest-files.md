---
title: "Puppet Manifest Files"
weight: 30
pre: "6. "
---

{{< youtube 3QFCLHACFIM >}}

#### Resources

* [Slides]({{< relref "/2-configuration-management/06-puppet-manifest-files-slides.md" >}})
* [Configuration Management 101: Writing Puppet Manifests](https://www.digitalocean.com/community/tutorials/configuration-management-101-writing-puppet-manifests) from DigitalOcean
* [Language: Visual Index](https://puppet.com/docs/puppet/5.5/lang_visual_index.html) from Puppet
* [Language: Basics](https://puppet.com/docs/puppet/5.5/lang_summary.html) from Puppet

#### Video Script

Now, let's take a look at how we can use Puppet to create defined configurations to be applied to our systems. In Puppet, we refer to those defined configurations as manifest files. Each manifest file defines a set of resources to be configured on the system. Then, the Puppet Agent tool compares the configuration defined in the manifest file and the system's current configuration, making changes as needed to the system until they match. In addition, each manifest file should be written in a way that it can be repeatedly applied to a system, since it is only defining the configuration desired and not the steps to accomplish it. This makes Puppet a very powerful tool for managing system configuration across a variety of systems and platforms.

When you apply a manifest file, Puppet will go through a compilation process to convert the manifest file into a catalog. When working in a larger organization with a Puppet master server containing several manifest files, this allows the system to distill all of that information into a single place. We'll talk a bit more about that when we look at a master/agent setup using Puppet.

Now, let's create our first Puppet Manifest files. Once again, I'm using the Learning Puppet VM during the `hello_puppet` quest, but you can follow along on your own Windows or Linux VM as well. I'll use SSH to connect to the `hello.puppet.vm` node, then make sure the Puppet Agent is installed.

To make this process simpler, I'm also going to install the Nano text editor. For most beginners, I feel that Nano is the easiest command-line text editor to learn, though it may not be the most powerful. If you are familiar with Vim, feel free to use it as it is already installed on this system. Since the Learning Puppet VM is using CentOS as its Linux distribution of choice, the command to install packages is a bit different than on Ubuntu. To install Nano, type the following:

```bash
sudo yum install nano
```

Now, let's open a new text file using Nano, called `manifest.pp`. In that file, we can define a file resource as follows:

```pp
file { '/tmp/testfile':
  ensure => 'file',
  content => 'Manifest File!',
  mode => '0644'
}
```

Once you have created that file, press <kbd>CTRL</kbd>+<kbd>X</kbd>, then <kbd>Y</kbd>, then <kbd>ENTER</kbd> to save and close the file in Nano. Then, you can apply the file using this command:

```bash
sudo puppet apply manifest.pp
```

It should successfully apply, and give you a message that the file was created. You can then use either

```bash
sudo puppet resource file /tmp/testfile
```

or

```bash
ls -l /tmp/testfile
```

to verify that the file exists and has the correct permissions. You can also view the file's contents using

```bash
cat /tmp/testfile
```

It's that easy! Most of the attributes displayed when you use the puppet resource command are configurable in a manifest file, so you can use puppet resource to determine how a system is currently configured, then copy the desired attributes into a manifest file to define that configuration. Let's add a few more things to our manifest:

```pp
package {  'nano':
  ensure => 'present'
}

user { 'cis527':
  ensure => 'present',
  shell => '/bin/zsh',
  home => '/home/cis527',
  managehome => true
}
```

Once you've edited a manifest file, you can verify that your syntax is correct using the following command:

```bash
puppet parser validate manifest.pp
```

If you have any errors in your manifest file, it will give you the approximate line and column number. Be careful about your use of colons, commas, quotes, and brackets. As with any programming language, Puppet is very particular about the correct use of syntax.

Now, let's apply that manifest and see what happens:

```bash
sudo puppet apply manifest.pp
```

Since the Nano package is already installed, it probably won't do much at this point. However, it should create the cis527 user. We can verify that it worked by switching to that user account. First, we'll need to set a password for it:

```bash
sudo passwd cis527
```

Then, we can use that password and the switch user command to log in as that user:

```bash
su cis527
```

If all goes well, our terminal should change to show that we are logged in as the cis527 user. Of course, it is possible to define the desired password in the manifest file, but that is something you'll have to figure out on your own as you complete Lab 2. (I can't give everything away, can I?)

Before moving on to the next video, I encourage you to play around with this temporary manifest file a bit and see what other changes you can make to the resources we've defined, or what other resources you can use here.
