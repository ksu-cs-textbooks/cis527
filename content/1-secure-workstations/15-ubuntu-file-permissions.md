---
title: "Ubuntu File Permissions"
weight: 75
pre: "15. "
---

{{< youtube WJShln4pEL0 >}}

#### Resources

* **[Slides]({{< relref "/1-secure-workstations/15-ubuntu-file-permissions-slides.md" >}})**
* [An Introduction to Linux File Permissions](https://www.digitalocean.com/community/tutorials/an-introduction-to-linux-permissions) from DigitalOcean
* [File Permissions](https://help.ubuntu.com/community/FilePermissions) from Ubuntu
* [Enable Open as Administrator on Ubuntu 18.04](https://websiteforstudents.com/enable-open-as-administrator-on-ubuntu-16-04-17-10-18-04/) from Website for Students
* [chmod](https://leanpub.com/jelinux/read#chmod) on Just Enough Linux
* [Linux Users and Groups](https://www.linode.com/docs/tools-reference/linux-users-and-groups/) on Linode

#### Video Script

In this video, we will discuss how file permissions work in Ubuntu Linux. Working with file permissions in Linux is sometimes one of the more challenging aspects of the operating system, as it is very limited compared to Windows. It requires a bit of thinking to determine how to configure your permissions, but if done correctly it can be very powerful.

Linux file permissions are assigned based on three classes of user: the owner of the file, the group assigned to the file, and all other users not included in those first two classes. Then, each class can get any combination of three file permissions: read, write, and execute. So, in essence, each file has 9 bits in its mode, determining which of the three permissions are assigned to each of the three classes.

To see these permissions, you can open a terminal and use the `ls -l` command. It will show a long listing (hence the `l`) of the files in the folder. You'll receive output very similar to this diagram, from the great tutorial on Linux file permissions from DigitalOcean, which is linked in the resources below the video. The first column gives the file permissions, known as the "mode" of the file. The next columns give the user and group assigned to the file, respectively. Following that, you'll find the file size in bytes, the last modified date, and the filename.

This graphic shows how the mode of the file works in detail. The first character is a `d` if the item is a directory, or a hyphen `-` if it is not. The next three characters give the read, write, and execute permission status for the user or owner of the file. The character is present if the permission is given, or a hyphen if it is not. The next three characters do the same for the group, then the last three for all other users.

Going back a bit, we can see that there are several different permission setups here in this graphic, with helpful filenames for each one to help us understand them. First, notice that the top two entries are for directories which are accessible either by everyone, or the group.

For users to be able to list the files inside of a directory, they must be given both the read and execute permissions, as we can see here in the eighth entry. If a user is given read permissions but not execute, they would be able to read files inside of the folder, but not able to get a listing of the files names, which isn't very useful. For files, the execute bit is only needed when the file is either an executable program, or a script written in a scripting language that is directly executable.

Looking through the rest of the entries, we can see what it would look like to have a file private to a user, or publicly accessible (though not writable) by all users. I encourage you to familiarize yourself with this pattern, as it will be very useful throughout this class.

File modes can also be expressed as a set of three octal characters. This is very useful if you have a firm understanding of what each octal mode represents. For each class of users, think of the three permissions, read, write, and execute, as three bits in a binary number. If read and execute are given, then the binary number is 101, which represents 5. That would be the octal value for that set of permissions. So, by using three octal values representing the permissions given to the three classes of user, it is very simple to set permissions using just three digits.

This page shows some common octal values you may use. I recommend reviewing it as you need while setting permissions. It is available in the slides linked below this video.

Now, let's see how to set these permissions using the tools available in Ubuntu Linux. First and foremost, you can do some work with permissions via the default file browser, called Nautilus. As in Windows, you can right-click on any file or folder, choose Properties, then click on the Permissions tab. Here, you can see several options to choose from. Each one should be pretty self-explanatory based on the information we've already covered in this video.

However, you'll notice that you can only change the permissions on files which you are the owner of. So, if you want to change the permissions of a file outside your home folder, for example, you won't be able to do so with Nautilus. There are a couple of ways around that, though. One is to install the `nautilus-admin` package. This will give you an option in Nautilus to right-click a folder or file and open it as an administrator using the `sudo` command. This will allow you to change the permissions all folders on the system, but it still does not easily allow you to change the owner or group assigned to those files.

For full control over file permissions, once again we must turn to the Terminal. There are several commands that are used to modify file permissions and owners. First is the `chmod` or "change mode" command. It is used to set the permissions on a file. The syntax is the command, followed by some type of descriptor for the permissions to be set, then the path to the file or folder to set those permissions on.

There are two ways to use this command. The first involves using the classes, permissions, and a set of operators to state how the permissions should be set. For example, `ug+rw` will add the read and write permissions to the user or owner of the file, as well as the group. You can also say `g=rx` to set the group permissions to be exactly read and execute, or `o-rwx` to remove all permissions from users other than the owner or the group. Finally, there is a special class, `a`, which represents all classes. So, `a+x` will give the execute permission to all classes of user.

In my opinion, I find that method simpler to understand in theory, but a bit more frustrating to work with in practice, because I have to explicitly spell out my permissions in a long-form manner to get exactly what I want. Thankfully, you can also specify the desired permissions using octal modes as well.

You can also use the `chown` command to change the owner or group assigned to a file. For this command, note that the user and group are separated by a colon, but no spaces are before or after the colon. Also, note that each file must have a group assigned to it, even if you only want the owner to have access. In that case, remember that each user account has a group of the same name, so you can assign that group as the group on the file as well.

Finally, there is also a `chgrp` command that allows you to change the group on a file you own. However, most users still just use the `chown` command for this use. However, if you do not have sudo access, this command is very useful.

Of course, in many instances you'll find that these commands require the use of the `sudo` command, In general, you can only change the permissions or group on a file you own without using `sudo`. Any other changes, including changing the owner of the file, require sudo access. It should also be noted that anyone with sudo access will in effect be able to access any file on the system. So, there is always a tradeoff between giving users the power to make exhaustive changes to file permissions and them being able to access any file on the system.

Now that you know a bit more about file permissions in Linux, you are ready to begin the next part of Lab 1 which is Task 6 - Ubuntu Files & Permissions. Good luck!
