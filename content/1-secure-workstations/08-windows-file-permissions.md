---
title: "Windows 10 File Permissions"
weight: 40
pre: "8. "
---

{{% notice warning %}}
_See the warning in the video script below for a correction that is not present in the video --Russ_
{{% /notice %}}

{{< youtube -OhecOPshA4 >}}

#### Resources

* [File and Folder Permissions](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/bb727008(v=technet.10)) from Microsoft
* [How to Understand Those Confusing Windows 7 File/Share Permissions](https://www.howtogeek.com/72718/how-to-understand-those-confusing-windows-7-fileshare-permissions/) from How-To Geek (applies to Windows 11)
* [How to Take Ownership and Change Permissions of Files and Folders](https://www.digitalcitizen.life/take-ownership-and-change-permissions-files-and-folders) from Digital Citizen
* [Advanced Security Audit Policy Settings](https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/advanced-security-audit-policy-settings) from Microsoft

#### Video Script

Now, let's take a look at file permissions in Windows 10. File permissions are very important in any computer system, as they control which folders and files each user is able to access. In this video, I'll go through some of the basics of configuring file permissions in Windows.

As demonstration, I've created a folder at the root of the C:\ drive, called test. Then, inside of that folder, I've created another folder called subfolder. This gives me a simple file hierarchy.

First, let's look at the permissions for the test folder. To find those, right-click on the folder and select Properties. Then, look at the Security tab. Here, you'll see a summary of the current file permissions. For this file, there are four groups listed:

* Authenticated Users - all but full control
* SYSTEM - full control
* Administrators - full control
* Users - read & execute, list contents, and read files

We'll examine each of the those permissions in detail as we make changes.

To make changes to permissions, there are two options. The first is to click the Edit button, which brings up a simple dialog for making changes, but does not include all options available. Therefore, I don't recommend using this interface unless you want to make very quick changes.

Instead, I recommend clicking the Advanced button below, to get a better idea of the options available.

At the top of this window, you can see the folder name, as well as the current owner of the folder. If you need to change the owner to a different user or group, you can click the Change link to do so.

On this window, there are three tabs. Let's look at the Permissions tab first. Here, you can see all the entries in the access control list, or ACL, for this folder.

In addition to the user or group and permissions, we can also see how the permissions are inherited. Windows permissions can be inherited from parent folders, and then those permissions can be applied to child folders and files as well.

In many cases, you won't need to change the inheritance of a folder, as you'll generally want to inherit the permissions that the system sets. However, you can disable inheritance by clicking the Disable Inheritance button at the bottom. When you do, it will ask you if you want to convert inherited permissions to explicit permissions, or remove them entirely. In most cases, I recommend always converting them to explicit permissions. You can always delete the unneeded ones later, but removing some of the inherited entries may make the folder inaccessible. Let's disable inheritance on this folder.

Before we make changes, let's look at the current permissions. I'm going to click on the entry for Administrators, then click Edit. Notice at the top of the window there is a Type option for either allow or deny. I always recommend using allow permissions, as that will give your permissions a consistency to how they are structured. If you feel that you must deny a permission, that is usually a good indication that you should rethink your users and groups to avoid such a scenario.

Below that, you can set where this permission applies. There are many options there, and most of them are pretty self-explanatory.

Finally, there are the basic permissions in Windows. Again, they are pretty self-explanatory. If you are unsure what a particular option does, I highly recommend consulting the Windows documentation. Also, note that you can click the Advanced Permissions link to the right to see more advanced permissions. In most cases, you won't use them, but they are available if needed.

Going back to the main dialog, there are two sets of permissions that I recommend not changing on ANY folder. First, each folder should have an entry for Administrators, giving that group full control of the folder. If, for any reason, you feel that your Administrators group should not have full control of a folder, you should rethink your permission structure. System administrators will need to have control of a folder in order to change the permissions, and most users should never be Administrators.

Likewise, do not modify the permissions of the SYSTEM group on any folders. That permission is vital for Windows services and processes to be able to perform operations on the folder.

One entry you may want to change is the entry for Authenticated Users. Currently, this entry allows any user with access to this system to access the folder or make changes. In essence, you can think of the Authenticated Users group as Everyone. In many cases, you'll want to remove that entry entirely, unless you want a folder to be publicly accessible on your system.

The last entry is for the Users group. This gives the permissions for any user not in the Administrators group. Again, you may or may not want to remove this entry, depending on your needs.

{{% notice warning %}}
**Correction:** By default, the Users group on Windows 10 contains the Authenticated Users group, so it actually includes all users on the system, not just those outside of the Administrators group. I don't recommend removing Authenticated Users from Users as it may have unintended consequences. Instead, you may want to make your own group for this purpose, and explicitly add all users who are not in Administrators to that group.
{{% /notice %}}

For this example, I'm going to remove the entry for Authenticated Users, but modify the entry for the Users group to allow users in that group to modify the contents of this folder.

Before clicking Apply, notice that there is a checkbox at the bottom to replace all child permissions with inheritable permissions from this object. If you would like to reset the permissions on folders within this one, you can use that option to do so. I'll do it, just to show you how it works. Of course, if there are several files or folders within this one, that operation could take quite a long time.

There are two other tabs to look at. The first one is the Auditing tab. Here, you can direct Windows to log events related to this folder, such as successful reads, writes, and more. Depending on your organization's needs, you may need to implement a strict auditing policy through this interface. We won't worry about it in this class, but I recommend reviewing the relevant documentation if you are interested.

The last tab, Effective Access, allows you to determine what the effective permissions would be for a particular group or user. This is a very useful tool, since users may be part of multiple groups, groups can be nested, and permissions can quickly become very convoluted. When in doubt, use this tool to make sure you have set the permissions correctly.

Once I am done here, I can click Apply, then click OK to apply my changes and exit the dialog.

Let's briefly look at the child folder's permissions, just to see what impact those changes had.

You can see that it now inherits permissions directly from its parent folder, as expected. From here, I can add additional permissions that are applicable to just this folder and all of its subfolders.

You should now be able to start working on Lab 1, Task 3 - Windows Files & Permissions. A large portion of that task involves creating a file structure with permissions as defined in the assignment. Make sure you read the instructions carefully, and post questions in the course discussion forum if you are unsure how to interpret a particular direction.
