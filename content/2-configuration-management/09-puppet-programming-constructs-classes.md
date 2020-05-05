---
title: "Puppet Programming Constructs & Classes"
weight: 45
pre: "9. "
---

{{< youtube 1-i6RDUoAeI >}}

#### Resources

* [Conditional Statements and Expressions](https://puppet.com/docs/puppet/latest/lang_conditional.html) from Puppet
* [Expressions and Operators](https://puppet.com/docs/puppet/latest/lang_expressions.html) from Puppet
* [Classes](https://puppet.com/docs/puppet/latest/lang_classes.html) from Puppet
* [Puppet Labs Standard Library](https://forge.puppet.com/puppetlabs/stdlib) from Puppet
* [Puppet Forge](https://forge.puppet.com/) from Puppet

#### Video Script

Puppet also has very powerful programming constructs which can be used in your manifest files. One of the most useful is the conditional statement, or "if" statement. The syntax is very similar to most other languages. For example, here is the sample "if" statement from the Puppet documentation:

```pp
if $facts['is_virtual'] {
  warning('Tried to include class ntp on virtual machine; this node might be misclassified.')
}
elsif $facts['os']['family'] == 'Darwin' {
  warning('This NTP module does not yet work on our Mac laptops.')
}
else {
  include ntp
}
```

In this statement, the manifest is determining if the system is virtualized, or if the OS family is Darwin, the base kernel family for Apple Macintosh laptops. If either of those is the case, it will print a warning message. However, if neither of those is true, then it will include the `ntp` module. We'll talk about modules later in the video. An "if" statement such as this, combined with the information that can be gleaned from a system using Facter, allows you to create manifest files that could be applied on a variety of different systems.

One caveat to be aware of: make sure you are careful about your data types. In Puppet, as in many other languages, the boolean value `false` and the string value `"false"` are different. In fact, Puppet treats non-empty strings as the boolean value true by default. In addition, all of the facts from Facter are strings, so you must be careful how you use them.

Consider this example:

```pp
$boolean = "false"
if $boolean {
  notify{"This is true":}
}
else {
  notify{"This is false":}
}
```

When you run a manifest file containing this code, you'll be notified that the value is true, since is a string. To resolve this problem, you can use the `str2bool` function included in the Puppet Labs Standard Library. First, install the Puppet Labs Standard Library module using the following command:

```bash
puppet module install puppetlabs-stdlib
```

Then, modify the manifest file as follows:

```pp
include stdlib
$boolean = "false"
if str2bool("$boolean") {
  notify{"This is true":}
}
else {
  notify{"This is false":}
}
```

Now, you'll get the expected result. The Puppet Labs Standard Library includes many other useful functions, so I encourage you to check them out. The documentation is linked in the resources below this video.

In addition to the "if" statement, Puppet also includes a "case" statement. The basic syntax is as follows:

```pp
case $operatingsystem {
  "centos": { $apache = "httpd" }
  "redhat": { $apache = "httpd" }
  "debian": { $apache = "apache2" }
  "ubuntu": { $apache = "apache2" }
  default: { fail("Unrecognized OS") }
}
```

The matches here are case-insensitive, which is very helpful. You can also combine some of the labels and use regular expressions, as in this example:

```pp
case $operatingsystem {
"centos", "redhat": { $apache = "httpd" }
/^(Debian|Ubuntu)$/: { $apache = "apache2" }
default: { fail("Unrecognized OS") }
}
```

When using regular expressions, note that the matching is case-sensitive.

Finally, Puppet code can be further organized into classes. As with most object-oriented languages, a class definition is very simple. Here is one example:

```pp
class myclass (String $message = "Hello") {
  notify { "${message} user": }
}
```

Once the class is defined, you can use the include keyword to declare it in your manifest file, using all default values for parameters:

```pp
include myclass
```

Or you may declare it using a resource syntax, allowing you to override default parameter values:

```pp
class { 'myclass':
  message => "Test"
}
```

Either way, it is important to remember that you must always declare a class to use it. A class definition itself is not sufficient for the resources inside the class to be configured.

Finally, on most enterprise Puppet systems, the manifest files have been further organized into a set of modules. Each module is a self-contained set of manifest files, templates, and configuration files, all for a particular use. For example, above the sample code references the `ntp` module, which is a module available from Puppet for managing NTP servers.

Unfortunately, writing your own modules is a very complex task, and I have decided that it is outside of the scope of what I'd like to cover in this class. Feel free to continue following the documentation in the Learning Puppet VM to see more about how to write your own modules.

In many cases, however, there are already modules freely available to perform a variety of common management tasks. So, I highly recommend checking out the available modules on Puppet Forge to see what's out there. As with many system administration tasks, don't try to reinvent the wheel if one already exists!
