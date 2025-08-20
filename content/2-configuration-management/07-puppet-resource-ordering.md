---
title: "Puppet Resource Ordering"
weight: 35
pre: "7. "
---

{{% notice info "Puppet Learning VM Deprecated" %}}

_As of 2023, the Puppet Learning VM is no longer being maintained. The videos below demonstrate some of the features of Puppet, which can also be done on your Ubuntu VM after installing Puppet Agent. Unfortunately, it is not easily possible to simulate an enterprise Puppet setup without this VM, so I'll keep these videos up for demonstration purposes._ --Russ

{{% /notice %}}

{{< youtube RywZUa_x3oA >}}

#### Resources

* [Language: Relationships and Ordering](https://help.puppet.com/core//current/Content/PuppetCore/lang_relationships.htm) from Puppet

#### Video Script

Now that we've seen Puppet Manifest files, let's discuss some of the caveats of such a system. On the Learning Puppet VM, during the `hello_puppet` quest as described in the earlier videos, I'm going to continue to create manifest files on the `hello.puppet.vm` node.

Using Nano, create the following manifest file:

```pp
file { '/tmp/test1':
  ensure => 'file'
}

file { '/tmp/test2':
  ensure => 'file'
}

file { '/tmp/test3':
  ensure => 'file'
}

notify { "First Notification": }
notify { "Second Notification": }
notify { "Third Notification": }
```

Once that is done, apply the manifest:

```bash
sudo puppet apply test.pp
```

When you do, you may see things applied out of order. Since a Puppet Manifest file only defines the desired configuration, it is up to the Puppet Agent tool to determine which steps are necessary and in what order. This is because Puppet considers each resource definition to be **atomic**, meaning that it is independent of all other resources. In some cases, however, we want to make sure that some resources are configured before others. Thankfully, Puppet gives us many ways to do so.

The first uses the before and require keywords. Here is an example from the Puppet documentation linked in the resources section below the video:

```pp
package { 'openssh-server':
  ensure => present,
  before => File['/etc/ssh/sshd_config'],
}

file { '/etc/ssh/sshd_config':
  ensure => file,
  mode => '0600',
  source => 'puppet:///modules/sshd/sshd_config',
  require => Package['openssh-server'],
}
```

Each of these elements creates the same relationship. You only need to include either the before or require keyword in one of the resources, but both are not required.

Similarly, the notify and subscribe keywords create a similar relationship. From the documentation:

```pp
file { '/etc/ssh/sshd_config':
  ensure => file,
  mode => '0600',
  source => 'puppet:///modules/sshd/sshd_config',
  notify => Service['sshd'],
}

service { 'sshd':
  ensure => running,
  enable => true,
  subscribe => File['/etc/ssh/sshd_config'],
}
```

Again, only one or the other is required. However, unlike with the before and require keywords, in this case the second item will only be refreshed if the prior resource has changed. In this example, if the `sshd_config` file is changed, then the `sshd` service will be restarted so it will read the newly changed file. This is a very powerful tool for making changes to configuration files and making sure the services immediately restart and load the new configuration.

Finally, the third method is through the use of chaining arrows. This tells the Puppet Agent to apply resources in the order they are written in the manifest. One of the most powerful and common uses of this is to create a "Package, File, Service" chain. Here is the example from the Puppet documentation:

```pp
# first:
package { 'openssh-server':
  ensure => present,
} -> # and then:
file { '/etc/ssh/sshd_config':
  ensure => file,
  mode => '0600',
  source => 'puppet:///modules/sshd/sshd_config',
} ~> # and then, if the previous file was updated:
service { 'sshd':
  ensure => running,
  enable => true,
}
```

This manifest will ensure the `openssh-server` package is installed first. Then, once it is installed, it will place the desired configuration file on the system. The first arrow with a simple hyphen creates a before/require relationship. Then, if that file is modified in any way, the second arrow, using a tilde `~` character, will enforce a notify/subscribe relationship and cause the `sshd` service to refresh.

As you work on your Puppet Manifest files for Lab 2, it is helpful to keep in mind that some resources may need to be chained together to work properly. However, do not try to chain together your entire manifest file, as that defeats much of the flexibility of Puppet itself.
