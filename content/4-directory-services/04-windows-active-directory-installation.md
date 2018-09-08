---
title: "Windows Active Directory Installation"
weight: 20
pre: "4. "
---

{{< youtube  >}}

#### Resources

* [Step-By-Step: Setting Up Active Directory in Windows Server 2016](https://blogs.technet.microsoft.com/canitpro/2017/02/22/step-by-step-setting-up-active-directory-in-windows-server-2016/) from Microsoft
* [Add User Accounts on Active Directory](https://www.server-world.info/en/note?os=Windows_Server_2016&p=active_directory&f=3) from Server-World
* [AD DS Installation and Removal Wizard Page Descriptions](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/deploy/ad-ds-installation-and-removal-wizard-page-descriptions) from Microsoft
* [NetBIOS](https://en.wikipedia.org/wiki/NetBIOS) on Wikipedia

#### Video Transcript

In this video, I'll go through some of the process of configuring a Windows Server 2016 VM to act as an Active Directory Domain Controller. The goal of this video isn't to show you all the steps of the process, but provide commentary on some of the more confusing steps you'll perform.

In general, I'll be following the two guides linked in the resources section below this video. The third guide gives quite a bit of additional information about each option in the Active Directory Domain Services installation wizard, and is a very handy reference as you work through this process.

First, I'll need to set a static IP address on this system. I'll be using the IP address ending in `42` for this server, which was reserved in in the DNS server configured in Lab 3. I'll also need to configure some static DNS entries. For a Domain Controller, you'll always want to make the first DNS entry the IP address of the server itself. This is because a Domain Controller also acts as a DNS server for the domain, so you'll need to tell this system to refer to itself for some DNS lookups. For the other entry, I'll use the VMWare router, which is the same as the default gateway address in my setup.

Next, I'm going to follow the steps to add the "Active Directory Domain Services" role to this server. This process is pretty straightforward, so I'll leave it to you to follow the guide.

---

Once the installation is complete, you'll be prompted to promote the server to a domain controller. This is the step where you'll actually configure the Active Directory installation. For this setup, we're going to create a new forest, using the `cis527.local` root domain name. You'll need to adjust these settings to match the required configuration for the lab assignment. By using a `.local` top-level domain, we can guarantee that this will never be routable on the global internet. The use of a `.local` suffix here doesn't actually comply with current DNS standards, but for our internal VM network it will work just fine. Of course, if you are doing this on an actual enterprise system, you may actually use your company's internet domain name here, with a custom prefix for your directory. For example, the K-State Computer Science department might use a domain name of `ldap.cs.ksu.edu` for this server.

Next, you'll need to configure the functional level of the domain. If you have older systems in your network, you will want to choose the option here for the oldest domain controller in the domain. Since we're just creating a new system, we can use the latest option here.

You'll also need to input a password here for Directory Services Restore Mode. In an enterprise setting, this is the password that you'll use if you ever have to restore your domain from a backup, or work with a domain controller that will not boot correctly. So, you'd generally make this a unique password, and store it in a safe location. For our example, I'm just going to use the password we've been using for all of our windows systems, but in practice you would make it much more secure.

Next are the DNS options. If you are running a separate DNS server in your organization, you'll need to checkmark this box to create a DNS delegation. However, for this lab assignment you won't need to do that, since we aren't trying to combine our Windows and Linux environments.

Following that, you'll need to configure the NetBIOS name for the domain. In general, this is just the first part of your fully domain name. NetBIOS is a very old protocol that is not commonly used, but some Windows systems will still use it to find resources on a network. You can just accept the default option here, unless a different name would be more reasonable.

In addition, you'll be able to configure the storage paths on your system. For this example, we'll just keep the default paths. However, on a production server, it might make more sense to store these on a different drive, just in case you have to reinstall the operating system in the future. These are the folders that store the actual database and information for the Active Directory domain.

Finally, you'll be able to review the options before applying them. If you'd like, you can click the "View script" button to view a PowerShell script that you could use to perform these steps on a Windows Server without a GUI installed.

With all the settings in place, you can continue with the configuration process. The first step is a prerequisites check to make sure that the server is able to complete the installation. You may get a couple of warnings about weaker cryptography algorithms and DNS server delegation, but you can ignore those for this example. If the prerequisites check is passed, you can click "Install" to install the service.

---

Once it has installed and rebooted, you'll notice that you are now prompted to log in as a domain user. On Windows systems, the domain name is shown before the `\`, followed by your username. So, in this example, it now wants me to log in as `CIS527\Administrator`. This is a different account than the Administrator account on the computer itself, which we were using previously. To log in as a local account, you can use the computer name, followed by a `\` and then the username. If you don't remember the computer name, you can click the "How do I sign in to another domain?" link below the prompt to find it. For now, we'll log in as the domain administrator account.

Once you've logged in, you'll need to create at least one user on the Active Directory domain. You can find the **Active Directory Users and Computers** application under the **Tools** menu on the Server Manager. Thankfully, adding a user here is very similar to adding a user in the Computer Management interface on a Windows computer. As before, make sure you uncheck the box labeled "User must change password at next logon" and checkmark the "Password never expires" box for now.

That should get the server all set up! Next, we'll look at adding a Windows 10 computer to your new Active Directory Domain.
