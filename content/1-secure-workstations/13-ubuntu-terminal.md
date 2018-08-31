---
title: "Ubuntu Terminal"
weight: 65
pre: "13. "
---

{{< youtube HaSQhIjp3Mg >}}

#### Resources

* [Using the Terminal](https://help.ubuntu.com/community/UsingTheTerminal) from Ubuntu
* [Advanced Command Line How To](https://help.ubuntu.com/community/AdvancedCommandlineHowto) from Ubuntu
* [Beginners/Bash Scripting](https://help.ubuntu.com/community/Beginners/BashScripting) from Ubuntu
* [Environment Variables](https://help.ubuntu.com/community/EnvironmentVariables) from Ubuntu
* [Cron How To](https://help.ubuntu.com/community/CronHowto) from Ubuntu
* [An Introduction to the Linux Terminal](https://www.digitalocean.com/community/tutorials/an-introduction-to-the-linux-terminal) from DigitalOcean
* [The Ultimate A to Z List of Linux Commands](https://fossbytes.com/a-z-list-linux-command-line-reference/) from Fossbytes
* [The Linux Command Line - A Complete Introduction](https://www.amazon.com/dp/1593273894/) by William E. Schotts Jr. on Amazon
  - [LinuxCommand.org](http://linuxcommand.org/) Companion Website
* [Linux Tutorial](https://ryanstutorials.net/linuxtutorial/) from Ryans Tutorials

#### Video Script

One of the most important features of the Linux operating system is the Terminal command line interface. One major design feature of Linux is that nearly every operation can be controlled via the command line, and in fact some operations can either only be performed or are much simpler to perform there.

To open the Terminal, click the Activities button and search for Terminal. I recommend adding it to the favorites panel by clicking and dragging the icon to the left side of the screen. You'll be accessing it very often throughout this class, so having quick access to the terminal is very helpful.

By default, Ubuntu uses Bash, the Bourne Again SHell, as the default shell in the terminal. There are many other shells available, so feel free to check them out and see if you find one you prefer. For this course, I will use Bash since it is the default.

Looking at the Bash terminal, there are a few bits of important information presented immediately in the command prompt, which is the text shown on the screen before the blinking cursor. First, shown here in the green text, is the current username, followed by the at `@` symbol, then the current computer name. This helps you keep track of which computer you are using, and which username you are currently logged in as. This becomes very important later, as you'll be controlling several servers using a remote terminal program.

Following the colon, you'll see in blue the present working directory. In this case, it shows the tilde `~` symbol, which represents the users home folder. You can use the `pwd` command to see the full path.

Finally, this prompt ends in a dollar sign `$`. That represents the fact that this terminal is not a root terminal, and doesn't have root permissions by default. A root terminal, such as one you can get by using the `sudo su` command, will have a pound or hash symbol `#` at the end of the prompt. You'll also notice that the colors are disabled in the root terminal, but that can easily be changed in the Bash configuration file.

Let's review some simple Linux terminal commands:

* `pwd` - shows the present working directory
* `cd` - change directory
* `ls` - list files
* `ls -al` - show all file details and permissions
* `mkdir` - make new directory
* `rmdir` - remove empty directory
* `rm` - remove file
* `rm -r` - recursively remove a folder
* `cp` - copy file or folder
* `mv` - move file or folder
* `touch` - create a file (by "touching" its entry in the file tree); existing files are unchanged except for updating the last accessed timestamp
* `cat` - concatenate (print) files
* `apropos` - find commands for a keyword
* `whatis` - find command descriptions
* `whereis` - find location of a command on the filesystem
* `man` - find command help

As we learned in PowerShell, the vertical pipe `|` character can be used to take the output of a command and use it as input to another command. Here are a few examples:

* `sort`
* `grep` - search for text
* `wc` - get word count

To edit files using the Terminal, I recommend using the `nano` command, as it is generally regarded as the simplest text editor available by default on most Linux systems. If you prefer to use `vim`, `emacs`, or another editor, you are encouraged to do so. Also, on a Linux system with a GUI installed, you can use `gedit` to open the graphical editor as well.

To edit a file, simply type `nano` followed by the name or path to the file to be edited. If it doesn't exist, it'll simply open a blank file. Once there, you can enter your information. Remember that Nano is a terminal program, so you cannot use the mouse to move the cursor, only the arrow keys on the keypad. At the bottom you'll see several commands you can use. The carat `^` character represents the <kbd>CTRL</kbd> key. So, `^O` would mean <kbd>CTRL</kbd>+<kbd>O</kbd> for the "Write Out" command.

To save a file, you can use <kbd>CTRL</kbd>+<kbd>O</kbd> to write it to the disk. It will ask you to confirm the filename before saving, and you can just press <kbd>ENTER</kbd> to accept the one presented. To exit Nano, use <kbd>CTRL</kbd>+<kbd>X</kbd>. If the file is unsaved, you will be asked to save your changes. Press <kbd>Y</kbd> to save the changes, then <kbd>ENTER</kbd> to confirm the filename. In practice, you'll become very used to the process of using <kbd>CTRL</kbd>+<kbd>X</kbd>, <kbd>Y</kbd>, <kbd>ENTER</kbd> to save and close a file in Nano.

By default, the Linux Terminal does not give you administrator, or "root" permissions, even though you may be using an administrator account. To use those permissions, a special command called `sudo`, short for "super user do," is used. By prefacing any command with the `sudo` command, it will run that command as the root user, provided you have permissions to do so, and can enter the correct password for the account. In essence, it is a way to "elevate" your account to the root account for a single command.

For example, to install a program on Linux, you must have root or sudo permissions. I can try to use the `apt-get update` command without it, but it will not work. By prefacing that command with `sudo` I can, but first I must enter the password to my account.

One quick trick - you can use `sudo !!` to run the previous command as root, without having to retype it. It is one of the single biggest timesaving tricks on the Linux terminal, and well worth remembering.

In addition, as I showed above, it is possible to switch to a root shell by using the `sudo su` command. Su is short for "switch user" and is used to change the user account on the terminal. You can use it to log in to any other account on the system, provided you know the password. However, I **DO NOT** recommend logging in directly as the root user in this way, as any command you accidentally type or copy/paste into this terminal will be run without any warning. It is very easy to irreversibly damage your system by doing so.

That is just a short introduction to the Linux terminal. We'll learn a few other terminal commands as we continue to explore Ubuntu. I also encourage you to read some of the resources linked below the video if you are new to Linux, as they give you much more information about the terminal and how it can be used.
