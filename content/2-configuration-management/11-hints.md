---
title: "Hints"
weight: 55
pre: "11. "
---

{{< youtube td6I_LDL91w >}}

#### Resources

* [Resource Type: User](https://help.puppet.com/core//current/Content/PuppetCore/Markdown/user.htm) from Puppet
* [Resource Tips and Examples: Package on Windows](https://help.puppet.com/core//current/Content/PuppetCore/resources_package_windows.htm) from Puppet
* [Managing Windows Configurations](https://www.puppet.com/docs/pe/2019.7/managing_windows_configurations.html) from Puppet
* [Puppet on Windows Pack](https://forge.puppet.com/puppetlabs/windows) from Puppet Forge
* [Installing and Using Windows Modules](https://www.puppet.com/docs/pe/2019.7/installing_and_using_windows_modules.html) from Puppet
* [download_file Module](https://forge.puppet.com/puppet/download_file) from Puppet Forge
* [Running Puppet's Commands on Windows](https://help.puppet.com/core//current/Content/PuppetCore/services_commands_windows.htm) from Puppet
* [Using User and Group on Windows](https://help.puppet.com/core//current/Content/PuppetCore/resources_user_group_windows.htm) from Puppet
* [puppetlabs-acl Module](https://forge.puppet.com/puppetlabs/acl) on Puppet Forge

#### Video Script

Here are a few hints for completing Lab 2, based on the struggles some students have had during previous semesters.

First, let's talk about passwords. On the Puppet documentation for the user resource type, it notes that on Linux, the password given in the configuration file must already be encrypted. Thankfully, it gives you some hints here on using built-in functions, or functions from the Puppet Labs Standard Library, to calculate the correct encrypted password. You can also use the Sensitive data type to redact the plain-text password from log files. Of course, on Windows, you can only use cleartext passwords.

Next, installing packages on Windows can be quite difficult without using a package management program such as Chocolatey. In the resources section below this video, I've included a few links describing the process for installing and managing packages in Windows in detail. In short, you'll need to be very careful about the title matching the actual `DisplayName` of the package, as well as the `install_options` to make them install silently. This may take a bit of trial and error to get it working correctly.

In addition, when you download the installation files for Windows, make sure you get the full installers and not the "stub" installer that just downloads the real installer in the background. Sometimes you have to dig a bit deeper on the vendor's website to find these. As stated in the assignment sheet, you may also choose to download the files using the `download_file` Puppet module. Either approach will work.

Another important note: on both Windows and Linux, changes to group membership do not take effect immediately. On Linux, the current user must log-out and log-in to see the change, whereas on Windows a reboot is required in most cases. Because of this, when testing your manifest files, you may find it necessary to apply the manifest, then logout/reboot and apply it again for all resources to be configured correctly. That is fine, provided that it works as intended on the second application.

Finally, you may find that defining permissions in Windows is difficult using the default file resource. You may choose to install the `puppetlabs-acl` module to configure Windows permissions directly. The resources section below the video includes a link to that module and its documentation as well. 

I hope these hints help you successfully complete Lab 2 with minimal frustration. As always, if you have any questions or run into any issues, please post on the course discussion forums before contacting the instructor. Good luck!
