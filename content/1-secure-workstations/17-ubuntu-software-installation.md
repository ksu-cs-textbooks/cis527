---
title: "Ubuntu Software Installation"
weight: 85
pre: "17. "
---

{{< youtube Y1XjikiWzuE >}}

#### Resources

* **[Slides]({{% relref "/1-secure-workstations/17-ubuntu-software-installation-slides.md"  %}})**
* [Install Additional Applications](https://help.ubuntu.com/lts/ubuntu-help/addremove-install.html) from Ubuntu
* [Use Synaptic for More Advanced Software Management](https://help.ubuntu.com/lts/ubuntu-help/addremove-install-synaptic.html.en) from Ubuntu
* [Apt-Get How To](https://help.ubuntu.com/community/AptGet/Howto) from Ubuntu
* [How Software Installation & Package Managers Work on Linux](https://www.howtogeek.com/117579/htg-explains-how-software-installation-package-managers-work-on-linux/) from How-To Geek
* [Snaps](https://docs.snapcraft.io/snaps/) from Snapcraft.io
* [Introduction to Snaps](https://ubuntu.com/core/services/guide/snaps-intro) from Ubuntu Tutorials

#### Video Script

Let's take a look at installing software on Ubuntu Linux. Before we install anything, here is some information about the types of files installed along with a typical application in Ubuntu.

First, the executable file itself is placed somewhere in the path of the system, usually in either `/usr/lib` or `/usr/bin`. This is equivalent to the .EXE file in Windows. Each application may also have some shared library or object files, which are typically placed in the `/usr/lib` folder.

The configuration and settings file for the application are usually placed in the `/etc` folder, with user-specific information placed in a dotfile in the user's home directory. To see those files, use the `ls -al` command to show all hidden files. By convention, any file or folder with a name beginning with a period `.` is hidden by default. These files are typically referred to as "dotfiles" and are used to store user-specific configuration information in the user's home folder. They are hidden by default just to prevent most users from ever touching them, but by including them directly in the user's home folder, they are more likely to be included in system backups. On Windows, this is roughly equivalent to the `AppData` folder in each user's home directory.

Finally, every application on Linux typically installs some sort of documentation in the `/usr/share` directory, which can be accessed using the `man` command. If required, it may also place a few scripts in the systemd directories so the appropriate service or daemon can be started automatically.

There are several methods to install software on Ubuntu, each with their own advantages and disadvantages. First, most users primarily will start with the Ubuntu Software Center. This is the equivalent of an "app store" for Ubuntu, and it gives quick and easy access to the most commonly used applications. However, many system and server packages are not visible here, and must be installed elsewhere.

The official Ubuntu documentation recommends installing the Synaptic Package Manager for those tasks. It can be installed via the Ubuntu Software Center and then used on its own. It will show you all packages available for your system, and you can easily install or manage them. One nice feature about Synaptic is the ability to see what files are installed by a package by simply right-clicking on an installed package and choosing Properties, then the Installed Files tab. You can compare this to the output from InstallWatch Pro on Windows.

Using Synaptic, you can also configure the software repositories your system is able to install software from. While most software you'll need is easily installed through the default repositories, you may find that adding or changing those repositories becomes necessary, and you can do so here.

Of course, you can also install and configure software using the command line. The most common way to do so is via the `apt`, or "Advanced Packaging Tool" command. In previous versions of Ubuntu this was the `apt-get` command, but the syntax for the `apt` command is exactly the same. To use `apt`, you must first update the list of packages available by using `sudo apt update`. Then, you can install a package using `sudo apt install <package>`. To remove a package, use the `remove` option. You can also use `apt` to upgrade all packages on a system using the `upgrade` option.

Another option for installing packages on Ubuntu is using the snap tool. Snaps are self-contained file system images containing the app and any dependencies, and are designed to be able to be installed on all major Linux systems. Several of the default Ubuntu packages are using snap, and the Ubuntu Software Center will list snaps if they are available. For this course, I will not be using snaps since they are not quite as widely supported yet, but feel free to review the relevant documentation listed in the resources section if you are interested in learning more.

In addition, you can always install software on Linux by downloading and installing the software package manually. The packages typically use the .DEB file extension, and are installed using the `dpkg -i` command. However, in most instances you'll be able to find a software repository which offers the software for installation via the `apt` tool, and I recommend using that route if at all possible.

Finally, if you so choose, you can download the source code for most applications built for Linux and compile it yourself. This is very rarely needed for most mainstream software, but often there is specialized software for a specific use that requires this level of work. In general, consult the documentation for that particular software for instructions on how to properly configure, build, install and run that software from source.

You should now be able to continue working on Lab 1, Task 5 - Configure Ubuntu 20.04 by installing the required software. As always, if you have any questions, please post in the course discussion forums to see if others are having the same issue.
