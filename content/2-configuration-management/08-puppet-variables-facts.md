---
title: "Puppet Variables & Facts"
weight: 40
pre: "8. "
---

{{< youtube SEVm33_GcYc >}}

#### Resources

* [Language: Variables](https://help.puppet.com/core//current/Content/PuppetCore/lang_variables.htm) from Puppet
* [Facter: Core Facts](https://help.puppet.com/core//current/Content/PuppetCore/Markdown/core_facts.htm) from Puppet
* [Values and Data Types](https://help.puppet.com/core//current/Content/PuppetCore/lang_data.htm) from Puppet
* [Templates](https://help.puppet.com/core//current/Content/PuppetCore/lang_template.htm) from Puppet

#### Video Script

In this video, we'll go just a bit deeper into the Puppet language and some additional features of Puppet. You may not need all of this information to complete Lab 2, but it is definitely helpful.

First, as with any programming language, Puppet allows you to assign variables. The basic syntax for assigning a variable is:

```pp
$my_variable = "Some text"
```

As with many scripting languages, a variable name always begins with a dollar sign `$`, and is assigned with a single equals sign `=`. Unlike most languages, however, variables can only be assigned once. If you think about it, this makes sense, since Puppet may apply resources in any order. In this way, it is much more of a declarative language than an imperative language, though it shares some features of both.

You can then use variables in your manifest files. For example, a variable is interpolated in any double-quoted string, such as here:

```pp
$username = "russfeld"
notify { "Your home directory is /home/${username}": }
```

Puppet also has a very powerful templating language that can be used with configuration files. It is outside the scope of what I'll cover in this class, but I encourage you to look into it on your own if you are interested.

Another tool bundled with Puppet is Facter. Facter is able to provide information about the system it is running on. Puppet can then use that information in manifest variables and templates to customize the system's configuration. To see the facts available on your system, type:

```bash
facter -p
```

Of course, you'll find that there are many facts available. You can find a full list of facts in the Puppet documentation linked below this video. You can also write custom facts, if needed.
