---
title: "Ubuntu Backups"
weight: 50
pre: "10. "
---

{{< youtube  >}}

#### Resources

* [Backing Up Files](https://help.ubuntu.com/stable/ubuntu-help/files.html.en#backup) from Ubuntu Documentation
* [Backups](https://help.ubuntu.com/lts/serverguide/backups.html.en) from Ubuntu Server Guide
* [How to Backup your Ubuntu Desktop with Déjà Dup](https://www.howtoforge.com/tutorial/ubuntu-backup-deja-dup/) from HowToForge
* [How to Create 'System Restore' Points in Ubuntu 18.04](http://tipsonubuntu.com/2018/03/17/create-system-restore-points-ubuntu-18-04/) from Tips on Ubuntu
* [How to Compress and Extract Files using the tar Command on Linux](https://www.howtogeek.com/248780/how-to-compress-and-extract-files-using-the-tar-command-on-linux/) from How-To Geek
* [How to Import and Export Databases and Reset a Root Password in MySQL](https://www.digitalocean.com/community/tutorials/how-to-import-and-export-databases-and-reset-a-root-password-in-mysql) from DigitalOcean
* [How To Backup MySQL Databases on an Ubuntu VPS](https://www.digitalocean.com/community/tutorials/how-to-backup-mysql-databases-on-an-ubuntu-vps) from DigitalOcean (steps should still be valid for 18.04)

#### Video Transcript

There are many different ways to back up files and settings on Ubuntu. In this video, I'll discuss a few of the most common approaches to creating backups on Ubuntu.

First, Ubuntu 18.04 includes a built-in backup tool, called "Déjà Dup," that will automatically create copies of specified folders on your system in the location of your choice. It can even store them directly on the cloud, using either Google or Nextcloud as the default storage location, as well as local or network folders. This feature is very similar to the File History feature in Windows 10.

In addition, many system administrators choose to write their own scripts for backing up files on Ubuntu. There are many different ways to go about this, but the resources from the Ubuntu Documentation site, linked below the video, give some great example scripts you can start with. You can even schedule those scripts using Cron, which is covered in the Extras module, to automatically perform backups of your system.

When backing up files on your system, it is very important to consider which files should be included. On Ubuntu, most user-specific data and settings are stored in that user's home folder, though many of them are included in hidden files, or "dotfiles." So, you'll need to make sure those files are included in the backup. In addition, most system-wide settings are stored in the `/etc` folder, so it is always a good idea to include that folder in any backup schemes. Finally, you may want to include data from other folders, such as `/var/www/` for Apache websites.

If you are running specific software on your system, such as MySQL for databases or OpenLDAP for directory services, you'll have to consult the documentation for each of those programs to determine the best way to back up that data. As part of this module's lab assignment, you'll be creating a backup of a MySQL database to get some experience with that process.

There are also some tools available for Ubuntu to help create backups similar to the System Restore feature of Windows. One such tool is TimeShift. I've linked to a description of the tool in the resources section below the video if you'd like to know more.

Finally, as with Windows, there are a large number of tools, both paid and free, available to help with creating, managing, and restoring backups on Ubuntu and many other Linux distributions. As you work on building a backup strategy for an organization, you'll definitely want to review some of those tools to see if they adequately meet your needs.

That concludes Module 7! As you continue to work on the lab assignment, feel free to post any questions you have in the course discussion forum on Canvas. Good luck!
