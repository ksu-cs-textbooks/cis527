---
title: "Ubuntu File Server"
weight: 30
pre: "6. "
---

{{< youtube  >}}

#### Resources

* [File Server](https://help.ubuntu.com/lts/serverguide/samba-fileserver.html.en) from Ubuntu Documentation
* [Samba Server Guide](https://help.ubuntu.com/community/Samba/SambaServerGuide) from Ubuntu Community Help Wiki
* [How to Set Up a Samba Share for a Small Organization on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-samba-share-for-a-small-organization-on-ubuntu-16-04) from DigitalOcean (works for 18.04)
* [Access User's Home Folders via Samba on Ubuntu 17.04](https://websiteforstudents.com/access-user-home-folders-via-samba-on-ubuntu-17-04-17-10/) from Website for Students (works for 18.04)
* [Mount Windows Shares Permanently](https://wiki.ubuntu.com/MountWindowsSharesPermanently) from Ubuntu Wiki
* [How Do I Access Windows Shares from Bash](https://askubuntu.com/questions/434358/how-do-i-access-windows-shares-from-bash) on Ask Ubuntu Forums
* [Use of pam-mount to Mount Home from Server](https://ubuntuforums.org/showthread.php?t=1375653) on Ubuntu Forums

#### Video Transcript

In this video, I'll walk you through the steps to set up a file server on Ubuntu using Samba. You'll learn how to share a particular folder, and I'll discuss what it takes to share the home folders for each user as well. Finally, I'll show you a bit of the process for making those shared folders available to your users on an Ubuntu client.

As before, I'll continue to use the VMs from Lab 4 for this example. Let's start on the server VM. First, if you haven't already, you'll need to install the Samba server:

```bash
sudo apt update
sudo apt install samba
```

Next, I'll need to create a folder to share, as well as a file in that folder just so it isn't empty:

```bash
sudo mkdir /shared
sudo touch /shared/file.txt
```

Finally, since that folder should be accessible to everyone, I'll set the permissions on that folder accordingly:

```bash
sudo chmod -R 777 /shared
```

Now that I have created my folder, I can work with Samba to share it with users on the network. There are a couple of different ways to accomplish this task. First, just like in Windows, you can right-click on the folder in Nautilus and access the sharing options there. For many users, this is the quickest and easiest way to share a folder on the network. However, for this example I'll show you how to share the folder directly in the Samba configuration file, which will give you a bit more control over the configuration.

So, let's open the Samba configuration file in Nano:

```bash
sudo nano /etc/samba/smb.conf
```

As you scroll through that file, you'll see that there are many different settings that you can customize on your Samba server. Pay special attention to the section for sharing user home directories, as that will be very useful as you complete the lab assignment later.

To add a new share, I'm going to add a few lines at the bottom of the file:

```conf
[shared]
  comment = Shared Files
  path = /shared
  browseable = yes
  guest ok = no
  read only = no
  create mask = 0755
```

Once you've made your edits, you should test your configuration file's syntax:

```bash
testparm
```

If everything looks as it should, then you can restart the Samba server to enable your new configuration:

```bash
sudo systemctl restart smbd
```

At this point, you may also need to adjust your firewall configuration to allow other systems on the network to access these shared resources. For this example, I have disabled my firewall for simplicity, but you'll need to make sure it is configured properly to receive full credit on your lab assignment.

Finally, we need to add users to our Samba server so they can access the resource remotely. Samba maintains a separate database of users since it cannot directly decrypt the password hashes stored in `/etc/shadow`, so it takes an extra step to enable our existing users to access shared resources via Samba. It is possible to configure Samba to use OpenLDAP for authentication, but the process is quite complex. I chose to leave that out of this exercise, but in an enterprise setting you may choose to do so.

To create and enable the `cis527` user in Samba, you can use the following commands:

```bash
sudo smbpasswd -a cis527
sudo smbpasswd -e cis527
```

The first command will ask you to enter a password for this user. This password can be different from the user's password on the system. However, I recommend setting this to be the same password that the user would use to login via LDAP or locally on their system. This will allow the system to automatically mount that user's home folder shared from Samba, as we'll see later in this video.

Now, let's switch over to our Ubuntu client and see how to access a shared folder. First, in Nautilus, you can click the **Other Locations** option on the left to see the available servers on the network. If network discovery is working properly, you may see your Ubuntu server listed there and be able to click on it.

If not, you can search for the server just like you would on Windows. At the bottom of Nautilus, there should be a **Connect to Server** box. In that box, you would enter `smb://` followed by the name or IP address of the system you'd like to connect to. So, in my example network, I would enter `smb://192.168.40.41` to find my server.

Once you can see the shares on the server, you can double-click a shared folder to mount it on your system. It should pop up a window asking for a username and password. If your shared folder supports guest access, you can select the "Anonymous" option at the top to open the folder as a guest user. Otherwise, choose the "Registered User" option and enter your Samba username and password in the appropriate boxes. You can generally leave the Domain box alone unless you have a specific domain or workgroup configured on your Samba server.

Also, note that if you enter the incorrect username and/or password, you might get a strange error stating "Failed to mount Windows share: File Exists." This error simply means that it was unable to access the shared resource, and most likely it is due to an authentication error. It isn't really a helpful error message, is it?

Once you've connected to the shared folder, you should see a shortcut to that folder appear on your Ubuntu desktop. You can also access that folder via Terminal, but it is quite buried. The folder is typically mounted in `/run/user/<UID>/gvfs/` where `<UID>` is the numerical user ID of your user on Ubuntu.

Thankfully, there are a few other ways to mount these shared folders on your system. First, using the Terminal, you'll need to install the `cifs-utils` package:

```bash
sudo apt update
sudo apt install cifs-utils
```

Then, you can mount that shared folder to the location of your choosing. I recommend first creating an empty folder in `/mnt` to act as a mount point:

```bash
sudo mkdir /mnt/shared
```

Then, you can use the `mount` command to mount the shared folder as a drive. For my example setup, I would use this command:

```bash
sudo mount -t cifs -o username=cis527,dir_mode=0777,file_mode=0777 //192.168.40.41/shared /mnt/shared
```

Of course, you'll have to adjust the command to fit your setup. Now, I can access those shared files at `/mnt/shared` in Terminal as well.

Once I am finished, I can unmount that share using the Terminal as well:

```bash
sudo umount /mnt/shared
```

To further automate this process, you can add an entry to the `/etc/fstab` file that gives the details for a shared folder that should be mounted automatically for each user on the system. You'll do just that for your lab assignment, so I won't cover the specific details here. As long as you are able to mount it using the commands above, it should be pretty straight-forward to adapt those settings to work in the `/etc/fstab` file.

Finally, you can also use `libpam-mount` to automatically mount drives on a per-user basis at login. This is especially useful if you want to automatically mount a user's home folder from a Samba server directly into their own home folder locally. To start, you'll need to install that library:

```bash
sudo apt update
sudo apt install libpam-mount
```

Next, you can configure it by editing its configuration file:

```bash
sudo nano /etc/security/pam_mount.conf.xml
```

As you look through that file, you'll see quite a few default options already in place. Unfortunately, since the file is in an XML format, it is a bit difficult to read. You'll need to make a couple of changes. First, look for the entry:

```xml
<debug enable="0" />
```

and change it to

```xml
<debug enable="1" />
```

to enable debugging. By doing so, you'll be able to see output in `/var/log/syslog` if this process doesn't work, and hopefully you'll be able to diagnose the error using that information.

Next, look for the line:

```xml
<!-- Volume definitions -->
```

and, right below that line, you'll add a line to define the shared folder you'd like to mount automatically. For my example setup, I would use the following definition:

```xml
<volume fstype="cifs" server="192.168.40.41" path="homes" mountpoint="/home/%(USER)/server" />
```

You'll have to adjust the options in that line to match your particular environment. Once you've added your information, save and close the file.

Next, we'll need to make sure that the system is configured to use that module. To do so, examine the `common-session` configuration file:

```bash
cat /etc/pam.d/common-session
```

and look for this line in that file:

```
session optional    pam_mount.so
```

If it isn't there, you'll need to add that line to the bottom of that file.

That should do it! To test your configuration, simply log out and log in again. If it works, you should now be able to see that user's home folder from the Samba server in the `server` folder in the home directory. It should also create shortcut on the Ubuntu desktop as well.

If it doesn't work, you'll want to review any error messages in the system log, The easiest way to find them is to search the system log for `mount` using the following command:

```bash
cat /var/log/syslog | grep mount
```

For the lab assignment, you'll perform these steps for your environment in much the same way. It can be very tricky to get this working the first time, so be very careful as you edit these configuration files. If you aren't able to get it working, please post in the course discussion forums on Canvas to get assistance.
