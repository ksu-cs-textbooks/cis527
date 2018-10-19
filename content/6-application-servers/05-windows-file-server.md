---
title: "Windows File Server"
weight: 25
pre: "5. "
---

{{< youtube kFagxkFgkkY >}}

#### Resources

* **[Windows Group Policy]({{< relref "/4-directory-services/06-windows-group-policy" >}})**
* [How to Share Files and Folders in Windows Server 2016](https://www.tactig.com/share-files-folders-windows-server-2016/) from Tactig
* [How to Map Network Drives with Group Policy (Complete Guide)](https://activedirectorypro.com/map-network-drives-with-group-policy/) by Robert Allen on Active Directory Pro
* [How to: Mapping Network Drives/Folders via Group Policy](https://community.spiceworks.com/how_to/79280-mapping-network-drives-folders-via-group-policy) on Spiceworks Community

#### Video Transcript

In this video, I'll briefly walk you through the steps of setting up a file server in Windows Server 2016, as well as how to access those resources from a Windows 10 client on the same network. Finally, I'll discuss a bit of information about how to automatically map those resource as network drives on the client using Group Policy.

First, let's take a look at our server. I'm using the same VMs from Lab 4 to continue this example. Your server probably already has the File Server role installed, but if not you can install it following the same process used to install the Active Directory Domain Services role in Lab 4.

In the Server Manger, you can click on the **File and Storage Services** role to view information about your server. There, you can see information about the storage volumes available on your server, as well as the shared folders. You should already see two shared folders on your system, named `NETLOGON` and `SYSVOL`. These are created for the Active Directory Domain Controller role, as they store important information about the domain, such as Group Policy Objects, or GPOs, that should be replicated to other systems on the domain. So, you shouldn't modify those shares!

If you'd like to create a new shared folder, the first step is to create that folder on your system. I'll just create a folder in the root of the `C:\` drive called `share`. I'll also create a simple text file in that folder, just so it isn't empty. Next, I can either right-click the folder and configure the sharing options there, or I can share it through the wizard in the Server Manager. I'll do the second option, since it gives me a bit more control over the configuration for the shared folder.

In that wizard, I'll choose the "SMB Share - Quick" option since I don't need to set any advanced settings. Next, I'll set the location of the shared folder. In this case, since I've already created it, I can click the **Browse** button at the bottom to select that folder. On the following screen, I can set some basic information about the shared folder, including the name and description of the share.

There are a few additional settings you can configure for the share, such as hiding files based on a user's permissions in the shared folder. I'll make sure I checkmark the option to "Encrypt data access" to protect any remote connections to this shared folder.

Next, you can set the permissions to access the share. To change them, click the **Customize Permissions** button. It is important to understand that a shared folder effectively has two sets of permissions - one set affecting access to the files and the folder itself, and another set, seen on the **Share** tab, that affects remote access to the files. In effect, you can limit who can access the files remotely, even if those users have permissions to access the files directly. I won't make any changes at this point, but for one of the shares in the lab assignment you may need to update the permissions at this point.

Finally, once everything is set correctly, I can click **Create** to create the shared folder. After it is created, I can see it in the Shares list inside the Server Manager.

There are a couple of ways to access the shared folder from a client on the same network. If network discovery is enabled, you can click the Network option on the left side of the Windows Explorer application to view servers on the network. However, in my experience, this option is usually the least successful, as Windows doesn't have a great history of being able to easily locate shared resources on the network.

Alternatively, you can always type two backslashes `\`, followed by either the computer name or IP address in the address bar of Windows Explorer to view the shares available on that system. So, for my example setup, I would enter either `\\cis527d-russfeld` or `\\192.168.40.42` to view the shares. I can then click on the shared folder name to view the files.

However, doing so might be a bit of a hassle for your users, so thankfully there are a few ways to make this process simpler. First, you can right-click on any shared drive and select the **Map Network Drive** option to create a mapped drive on your computer. In effect, this creates a shortcut in Windows Explorer directly to the shared folder, and it will assign it a drive letter just like the local disks on your system. For many users, this is a very simple way to make those network resources available.

However, you'd have to do this process manually for each user who would like to have the network drive mapped, and on each computer they would access it from. That seems very inefficient, right? Thankfully, there is an even better way to handle this using a Group Policy Object.

In the Group Policy editor, there is an option to create drive maps as part of a Group Policy Object. Here, I've configured a drive map to map that shared drive. Notice that I'm referencing it by IP address instead of the server name. This helps the system find the drive quickly, since that IP address should always work without needing to query the domain to find the server on the network.

Once I've created and enforced that Group Policy on the domain, I can switch back to the client and see if it works. One way to do so is to simply reboot the client and then log in again. When it reboots, it should receive the updated Group Policy Objects for the domain. However, if you'd like to test it immediately, you can open a Command Prompt or PowerShell window, and use the command `gpupdate /force` to force a Group Policy update from the Domain Controller.

Once you've updated the Group Policy, you should now see your newly mapped network drive in Windows Explorer. That's all it takes! From there, you should be able to complete the Windows File Server portion of Lab 6. Make sure you pay special attention to the permissions for each shared folder. You may also want to review the information from Module 5 regarding Windows Group Policy for a quick refresher.
