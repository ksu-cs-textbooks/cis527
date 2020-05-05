---
title: "Installing Puppet"
weight: 20
pre: "4. "
---

TODO

{{< youtube F12XwpusumA >}}

#### Resources
* [Puppet Agent Windows Downloads](https://downloads.puppetlabs.com/windows/puppet6/) from Puppet (look for puppet-agent-x64-latest.msi)
* [About Puppet Platform and Its Packages](https://puppet.com/docs/puppet/latest/puppet_platform.html) from Puppet
* [Puppet Learning VM](https://puppet.com/download-learning-vm) from Puppet
* [Puppet System Requirements](https://puppet.com/docs/pe/latest/system_requirements.html) from Puppet
* [Puppet Documentation](https://puppet.com/docs) from Puppet
* [Installing Puppet Agent](https://puppet.com/docs/puppet/latest/install_agents.html) from Puppet
* [Add Executables to your PATH](https://puppet.com/docs/puppet/latest/install_agents.html#concept-6837) from Puppet

#### Video Script

To begin work on Lab 2, you'll need to install Puppet Agent on your new VMs. This video will walk you through that process.

First, let's look at installing Puppet Agent on Ubuntu. Here I have an Ubuntu VM configured as described in the Lab 2 assignment, except I have not installed the Puppet Agent software yet. To install Puppet Agent, we must first enable the Puppet Platform repositories. A link to these instructions are in the resources section below the video. On that page, scroll down to the section titled "Enable the Puppet Platform on Apt" and enter the two commands given. 

However, we'll need to determine the URL required for our version of Puppet and Ubuntu. In this case, we'd like to install Puppet version 6, and we are using Ubuntu 20.04, which is codenamed "Focal Fossa". So, our URL would consist of 'puppet6' as the platform name, and 'focal' as the OS abbreviation. So, the full URL will be `https://apt.puppetlabs.com/puppet6-release-focal.deb`. When we place that first URL after `wget` in the first command, it will simply download a .DEB installation file to your computer. The second command uses the `dpkg` tool to install that file.

Once we've done that, we can use `sudo apt update` and `sudo apt install puppet-agent` to install the Puppet Agent program on Ubuntu. 

However, you won't be able to use those commands until we add them to the `PATH` environment variable. The `PATH` variable is a list of folders that contain the commands you can access from the Terminal. If you have reviewed the information in the Extras module for Bash Scripting, you are already familiar with the `PATH` variable. The instructions for installing Puppet Agent on Linux linked in the resources section gives one way to add these commands to your `PATH` variable, but it is incomplete and will not work in all cases. So, there are two options: one would be to use the full path each time you need to use the Puppet commands, and the second is to modify the `PATH` variable. In this video, I'll walk you through the steps to modify your `PATH` to enable direct access to these commands.

First, you must add it to your own `PATH` variable. To do so, use the following command to edit your Bash configuration file:

```bash
nano ~/.bashrc
```

Use the arrow keys to navigate to the bottom of the file. Then, on a new line, add the following:

```bash
export PATH=/opt/puppetlabs/bin:$PATH
```

Then press <kbd>CTRL</kbd>+<kbd>X</kbd>, then <kbd>Y</kbd>, then <kbd>ENTER</kbd> to save and close the file. Finally, close and reopen Terminal to load the new `PATH` variable. If you did it correctly, you should be able to run the `puppet` command, as you can see here.

However, if you try to use `sudo` to run the `puppet` command as root, you'll notice that it still cannot find the command. This is due to the fact that the system protects the `PATH` variable from changes when using root privileges in order to enhance system security. So, you'll also need to edit the `PATH` variable used by the `sudo` command. To do so, use the following command to open the `sudo` configuration file:

```bash
sudo visudo
```

This command will open the `\etc\sudoers` file on your system for editing. Near the top, you'll see a line for `Defaults secure_path` containing the `PATH` variable used by the `sudo` command. Carefully edit that line by adding the following text to the end, before the closing quotation mark:

```bash
:/opt/puppetlabs/bin
```

Note that I added a colon to the end of the existing line, then the new path. On my system, the full line now looks like this:

```bash
Defaults    secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin:/opt/puppetlabs/bin"
```

Once you are done editing, you can use <kbd>CTRL</kbd>+<kbd>X</kbd>, then <kbd>Y</kbd>, then <kbd>ENTER</kbd> to save and close the file. You should now be able to use the `sudo puppet` command as well.

Now, let's switch over to Windows and install the Puppet Agent there. First, you'll need to download the Puppet Agent using the link on the resources page below this video. Remember to find the latest version of the Puppet Agent installer, as there are many listed on this page. Once you have downloaded the file, simply double-click on it to run the installer. It will install Puppet Agent on the computer. It's that simple!
