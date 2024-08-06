---
title: "Windows 10 User Management"
weight: 35
pre: "7. "
---

{{< youtube pWGMXjMZM7w >}}

#### Resources

* **[Slides]({{% relref "/1-secure-workstations/07-windows-user-management-slides.md"  %}})**
* [Manage User Accounts in Windows](https://support.microsoft.com/en-us/windows/manage-user-accounts-in-windows-104dc19f-6430-4b49-6a2b-e4dbd1dcdf32) from Microsoft
* [How to manage user account settings on Windows 11](https://www.windowscentral.com/software-apps/windows-11/how-to-manage-user-account-settings-on-windows-11) from Windows Central
* [Understanding and Managing User Accounts in Windows 11](https://geekflare.com/user-accounts-in-windows-11/) from Geekflare
* [The Geek's Way of Managing User Accounts and Groups in Windows](https://www.digitalcitizen.life/geeks-way-managing-user-accounts-and-groups?utm_source=7tutorials.com&utm_medium=redirect&utm_campaign=7_Tutorials_Redirect) from Digital Citizen

#### Video Script

Once you have installed Windows 10, the next step is to configure the user accounts and groups needed on the system. There are three major methods for configuring user accounts, and each give you access to different sets of features. They are the Settings menu, the Control Panel, and the Administrative Tools. Let's look at each one.

First, the Settings menu. To find it, go to the Start Menu and select Settings. On the Settings menu, click Accounts. From here, you can click the Sign-in Options link to change your own password and other options. You can also click the Family & other users option to add additional users to the computer. However, by default it will ask you to provide the phone number or email address for a Microsoft account. To add a local account, you must first click the "I don't have this person's sign-in information" link, then "Add a user without a Microsoft account" to get to the correct screen. From there, you can simply set a username and password for that account.

Once the account is created, you can change the account type. Through the Settings menu, you are only given the option to create standard users and administrators.

Now, let's look at using the Control Panel to manage user accounts. To find the Control Panel, search for it on the Start Menu. You can also right-click the Start Button to access the Control Panel. Once there, click the User Accounts option twice to get to the User Accounts screen. From here, you can change your account name, something you aren't able to do from the Settings menu. However, it does not change the username, just the name displayed on the screen. You can also change your own account type here.

However, for most options such as creating a new account, it will refer you back to the Settings menu. There are a few options on the left side of the User Accounts screen that are difficult to find elsewhere, but they are rarely used. The most important one is the ability to create a password reset disk, which is a flash drive that can be used to reset a lost password. However, as we'll see later in the semester, resetting Windows passwords is trivial provided the disk isn't encrypted.

Finally, let's look at using the Administrative Tools to manage user accounts. The easiest way to access these is to right-click on the Start Button and select Computer Management. On that window, you'll see Local Users and Groups in the tree to the left, under System Tools. Expanding that option will give you access to two folders: Users and Groups. In the Users folder, you'll see all available user accounts on the system.

You'll notice that there are a few more accounts listed here than anywhere else, because Windows 10 includes several disabled accounts by default. The first, Administrator, is the actual built-in administrator account on the system. You can roughly compare it to the "root" account on a Linux computer. It has full access to everything on the system, but is disabled by default. Also, it has no password by default. This can create a major security hole, as it could be accidentally (or intentionally) enabled, giving anyone full access to the system. Most organizations choose to set a password on the account as a precaution, but leave it disabled.

The second, DefaultAccount, is simply a dummy account which stores the default profile. A copy of this account is made when each new user account is created. Using some tools available from Microsoft, it is possible to customize this account to give each user on the system a set of default settings, such as a desktop background.

The last default account, Guest, is the built-in guest account. It can be enabled to allow guests to access the computer. They can run programs, surf the internet, and store files in their folder, but generally cannot access any other user's folders, install software, or change any system configuration. If you must allow guest access to a computer, this is probably one of the better ways to do so.

Going back to Windows, you can create a new user account here very easily. However, there are a few things to be aware of when doing so. First, you can give it a name, username, and password. At the bottom, you'll see several checkboxes. The first one forces the user to change her or his password when first logging on to the system. I generally recommend not enabling this option, because that will also force the user's password to expire after a set time. Instead, I recommend unchecking that box, and checking the third one to set the password to never expire. If you would like to enforce password expiration, it is much better to do so using a central directory service such as Active Directory, which we'll cover in more detail in Module 4.

Once you have created a user account, you can right-click on it to edit a few properties. Notice that by right-clicking any account, you are given the option to set the account's password. This is helpful if a user has forgotten the account password and does not have a reset disk available. However, if the user has made use of Windows file encryption or some other security features of Windows, it may irrevocably destroy their ability to access that information. So, I only recommend using this feature as a last resort.

Looking at a user's properties, you can see tabs at the top to configure group memberships and profile information. On the Member Of tab, you can add users to different groups. Notice by default that users are only added to the Users group. If you'd like a user account to be an administrator, you'll have to manually add that user to the Administrators group here.

The profile tab gives additional options for the user account, such as defining a custom location for the user's profile, home folder, or scripts. However, I recommend not configuring these options on a local computer account. Instead, you can manage these from Active Directory. We'll cover that in Module 4.

Next, let's look at the Groups folder. Here you'll see several of the groups listed that are included in Windows 10 by default. The three groups to pay attention to are Administrators, Users, and Guests. They correspond to administrator accounts, normal user accounts, and guest accounts. By adding an account to one of those groups, you'll give it those permissions on the system. There are several other groups available, most of which are not used directly. If you'd like to know more about these groups, consult the relevant Windows documentation. Of course, you can create groups and manage group members from this window as well.

Lastly, let's briefly look at the User Account Control, or UAC, feature of Windows. You've probably seen this pop up from time to time if you use Windows regularly. UAC is used to prevent accounts from changing system settings without getting explicit confirmation of the change from someone with administrator privileges. I recommend leaving UAC at the default setting, as it will prevent malicious programs from making changes to your computer without alerting you first. On earlier versions of Windows, this was a major problem. You can compare this feature to how Mac and Linux computers constantly ask for an administrator account's password whenever software is installed or system settings are modified.

Finally, one other thing to look at is the Local Group Policy Editor on Windows. You can find it by searching for it on the Start Menu. This allows you to view and edit the local security policy of your system. For example, let's go to Windows Settings > Security Settings > Account Policies > Password Policy. Here, I could set policies regarding how often passwords must be changed, how long they must be, and whether they should meet certain complexity requirements. However, as I mentioned before, it is best to leave the local group policy alone, and instead configure group policies using Active Directory. We'll cover that in Module 4.

With this information, you should be able to start Lab 1, Task 2 - Configuring Windows 10. The next pages will continue giving you the information needed to complete that task.
