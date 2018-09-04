---
title: "Ubuntu User Management"
weight: 70
pre: "14. "
---

{{< youtube 1m_TT6sUuUw >}}

#### Resources

* **[Slides]({{< relref "/1-secure-workstations/14-ubuntu-user-management-slides.md" >}})**
* [User Accounts](https://help.ubuntu.com/lts/ubuntu-help/user-accounts.html) from Ubuntu
* [User Management](https://help.ubuntu.com/lts/serverguide/user-management.html) from Ubuntu Server Guide
* [How to Add and Delete Users on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-ubuntu-16-04) from DigitalOcean (Works for 18.04)
* [Gnome System Tools Package](https://launchpad.net/ubuntu/bionic/+package/gnome-system-tools) from Launchpad
  - Install this package to get the GUI to manage Users and Groups
* [The Beginner's Guide to Managing Users and Groups in Linux](https://www.howtogeek.com/howto/36845/the-beginners-guide-to-managing-users-and-groups-in-linux/) from How-To Geek
* [Linux Users and Groups](https://www.linode.com/docs/tools-reference/linux-users-and-groups/) from Linode

#### Video Script

In this video, we'll explore how to work with users and groups in Ubuntu Linux. Before we do that, however, let's take a minute to discuss some important information about user accounts and how they are managed in Linux.

Every Linux system has a special user account called "root." This account is the default system administrator account, and it has complete control over the system. It is easily identifiable by its UID, which is always 0. In fact, when many programs see that the current UID is 0, they will skip any and all permissions checks without looking at anything else.

On Ubuntu, the root account is disabled by default. It can easily be enabled by setting a password on the account using the `passwd` command on the Terminal. However, that is not recommended, as it makes your system more vulnerable to some kinds of attacks. Instead, the system provides the `sudo` command to allow regular users with administrative permissions to perform commands as the root user, without actually using that account.

The `sudo` command stands for "Super User Do" and is by far one of the most important commands to learn as a system administrator. By prefacing any command with `sudo` while using an account with the appropriate permissions and providing the account's password, you can become the root user while that command is running. To give users the ability to use `sudo` they simply must be added to the "sudo" group or have their user type set to Administrator.

You can also customize how the permissions for `sudo` are configured by using the `visudo` command to edit the `/etc/sudoers` file. For example, you can limit which commands certain accounts are able to perform. Be very careful, as that file has a very specific format and any invalid changes could render the entire system unusable. I generally don't recommend editing this file unless necessary.

As you configure Ubuntu accounts, you'll notice that there are three major account types. The first type, Regular User, consists of two sub-types - Standard and Administrator. These accounts are the ones that will be used by real people logging-in to the system interactively. Standard users do not have access to the `sudo` command, while Administrator users do. The regular users typically have a UID starting at 1000 and above, and each one has a group of the same name created with that user as the only initial member. This is very important for assigning file permissions, as we'll see in a later video. They also receive a skeleton of the default directory in the `/home` folder. As you learn about directory services in Module 4, you'll find this information to be helpful once again.

The other type of user, System User, is a user account created for a program or service. These are similar to the pseudo accounts on Windows 10, but on Ubuntu there are typically several of them, with a unique account assigned to each service. For example, the Apache web server which will be installed as part of this module creates its own user account, which can be used to determine what files can be accessed or served by the web server.

Now, let's look at the different ways user accounts can be configured on Ubuntu. First, we can go to the Settings application. From there, click the Details button on the left, then Users. Here you can see information about your current user account, and are able to change the password. You cannot change the user account type of the current account. To add a new account, you must click the "Unlock" button at the top of the screen and enter your current password. This is the graphical equivalent of using a `sudo` command. From there, you can create a new user.

You can also install the `gnome-system-tools` package to get access to a different interface for managing user accounts. Once it is installed, you can search for "Users and Groups" after clicking the activities button to find it. Here, you can add or edit accounts, and you can also manage existing groups. However, you are still unable to add users to groups or do any advanced editing here. To do most of that, you'll need to use the terminal.

There are several terminal commands which are useful. First, the `adduser` command will walk you through the process of adding a user to the system. This utility is not part of the default Linux system tools, but has been added to Debian and Ubuntu to simplify the process of adding a regular user. To add a system user, user the `useradd` command. You can also use commands to remove or modify a user. For example, to add a user to an existing group, use `usermod -a -G <group> <user>`.

Finally, you can also use the `passwd` command to change the password for any user account.

To work with groups, very similar commands are available. You can add a group using `groupadd` by providing a name for the group, as shown here. There are also a couple of commands for setting passwords and security for groups, which are shown in italics on the slides. Those commands are not typically used, but if you are interested in them I encourage you to review the resources below the video to learn more.

One important aspect of working with the Linux operating system is that most system settings and information are stored in simple text files, and anyone with access to those files can see how the system is configured. Let's take a look at the 4 most important ones.

First, `/etc/passwd` is the traditional place to find information about a user account. It includes the username, UID, home folder location, and more. It used to include a hash of the password as well, but that was removed years ago because it was a security threat.

Those passwords were moved to `/etc/shadow`, which you'll notice is a very protected file. In fact, I can only access it by using the `sudo` command. Here you'll see the hash of the cis527 user account we are using.

Similarly, there are `/etc/group` and `/etc/gshadow` files, serving the same purpose for groups.

Of course, it should go without saying that it is not recommended to edit those files directly. Instead, use the appropriate terminal commands to modify information about user accounts and groups.

At this point, you should be ready to start working on Lab 1, Task 5 - Configure Ubuntu 18.04. One of the first tasks in that lab is to create several user accounts, so that will be great practice for using some of these tools and commands.
