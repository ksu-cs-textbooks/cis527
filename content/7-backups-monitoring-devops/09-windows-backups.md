---
title: "Windows Backups"
weight: 45
pre: "9. "
---

{{< youtube -QDXQNNVtY0 >}}

#### Resources

* [How to Back Up Windows 10](https://www.techadvisor.co.uk/how-to/windows/how-back-up-windows-10-3635397/) from Tech Advisor
* [How to Use All of Windows 10's Backup and Recovery Tools](https://www.howtogeek.com/220986/how-to-use-all-of-windows-10%E2%80%99s-backup-and-recovery-tools/) from HowTo Geek
* [How to Make a Full Backup of your Windows 10 PC](https://www.windowscentral.com/how-make-full-backup-windows-10) from Windows Central

These resources mostly refer to Windows Server 2012 or 2016, but should work for 2019 as well. 

* [AD Forest Recovery - Backing up a full server](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/manage/ad-forest-recovery-backing-up-a-full-server) from Microsoft Windows IT Pro Center
* [How to Backup Active Directory Fully in Windows Server 2016](https://www.tactig.com/backup-active-directory-windows-server/) from Tactig
* [How to perform Authoritative Restore of Active Directory Objects - 2012 R2](http://www.itingredients.com/perform-authoritative-restore-active-directory-objects-2012-r2/) from ITIngredients (should work for 2016)
* [Windows Server 2012 - Active Directory - Backup and Restore, Part 1: System State](http://davidmtechblog.blogspot.com/2014/01/windows-server-2012-active-directory_10.html) from David M Tech Blog (should work for 2016)

#### Video Transcript

Windows includes several tools for performing backups directly within the operating system. In this video, I'll briefly introduce a few of those tools.

First is the Windows File History tool. You can find it in the **Settings** app under **Update & Security**. Once there, choose the **Backup** option from the menu on the left. To use File History, you'll need to have a second hard drive available. It can be either another internal drive, another partition on the same drive, or an external hard drive or flash drive. Once it is configured, File History will make a backup of any files that have changed on your system as often as you specify, and it will keep them for as long as you'd like, provided there is enough storage space available. By default, it will only back up files stored in your user's home directory, but you can easily add or exclude additional folders as well.

Right below the File History tool is the Backup and Restore tool from Windows 7. This tool allows you to create a full system image backup and store it on an external drive. This is a great way to create a single full backup of your system if you'd like to store one in a safe location. However, since Windows 10 now includes options to refresh your PC if Windows has problems, a full system image is less important to have now than it used to be.

However, one tool you may want to be familiar with is the System Restore tool. Many versions of Windows have included this tool, and it is a tried and true way to fix some issues that are caused by installing software or updates on Windows. You can easily search for the System Restore tool on the Start Menu to find it. In essence, System Restore automatically creates restore points on your system when you install any new software or updates, and gives you the ability to undo those changes if something goes wrong. System Restore isn't a full backup itself, but instead is a snapshot of the Windows Registry and a few other settings at that point in time. If it isn't enabled on your system, I highly recommend enabling it, just for that extra peace of mind in case something goes wrong. As a side note, if you've ever noticed a hidden folder named "System Volume Information" in Windows, that folder is where the System Restore backups are stored. So, I highly recommend not touching that folder unless you really know what you are doing.

In the rare instance that your operating system becomes completely inoperable, you can use Windows to create a system recovery drive. You can then use that drive to boot your system, perform troubleshooting steps, and even reinstall Windows if needed. However, in most instances, I just recommend keeping a copy of the standard Windows installation media, as it can perform most of those tasks as well.

Windows also has many tools for backing up files to the cloud. For example, Windows has Microsoft's OneDrive software built-in, which will allow you to automatically store files on your system in the cloud as well. While it isn't a true backup option, it at least gives you a second copy of some of your files. There are many other 3rd-party tools that perform this same function that you can use as well.

Finally, Windows Server includes the Windows Server Backup tool, which is specifically designed for the types of data that might be stored on a server. You can use this tool to create a backup of your entire server, including the Active Directory Domain Services data. Losing that data could be catastrophic to many organizations, so it is always recommended to have proper backups configured on your domain controllers. As part of the lab assignment, you'll use this tool to backup your Active Directory Domain, and then use that backup to restore an accidentally deleted entry, just to make sure that it is working properly.

Of course, there are many other backup tools available for Windows, both free and paid, that offer a variety of different features. If you are creating a backup strategy for your organization, you may also want to review those tools to see how well they meet your needs.
