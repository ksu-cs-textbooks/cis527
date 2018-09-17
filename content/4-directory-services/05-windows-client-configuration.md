---
title: "Windows Client Configuration"
weight: 25
pre: "5. "
---

{{< youtube  >}}

#### Resources

* [How to Join a Windows 10 PC to a Domain](https://www.groovypost.com/howto/join-a-windows-10-client-domain/) from groovyPost

#### Video Transcript

Once you have completely set up your Active Directory Domain, you can begin to add Windows clients to the domain. This video will walk through some of that process, and I'll discuss a few of the steps as we go.

For this example, I have my Windows 10 VM from the earlier labs. It is on the same network as the domain controller. Before I begin, I'll need to set some static DNS settings on this computer. First, and most importantly, I'll add a DNS entry for the domain controller first, and the second entry can be any of the other working DNS servers on the network. In this case, I'll just use the VMware default gateway.

Next, I'm going to right-click on the Start button and choose the System option. Before adding it to the domain, I need to make sure it is named correctly. If not, I'll need to rename it and reboot before adding it to the domain. Once a computer is on a domain, it is very difficult to rename it.

Once I'm sure it is correct, I'm going to click the **System Info** link to get to the old System options in the Control Panel. Here I should be able to see the current workgroup. To add the system to a domain, click the **Change settings** button to the right of the computer name. Then, I'll click the **Change** button to add it to the domain.

On this window, I'll choose the **Domain** option, and enter the name of the domain, in this case `cis527.local`, and click OK. You may get a message about the NetBIOS name of the computer being too long, but you can safely ignore that message.

If everything works correctly, you should see a pop up asking you to enter the username and password of an account with permissions to add a computer to the domain. In this case, the only account we've set up with those permissions is the domain administrator account, so we'll enter those credentials here. Once you enter it, it should welcome you to the domain, and prompt you to restart.

If your computer is unable to contact the domain at this step, it is usually a problem with your network configuration. To diagnose the problem, try to ping the domain name using the command-line `ping` utility and see what the response is. If it cannot find it, then check your network settings and DNS settings and make sure you can ping the domain controller as well. In many cases, this can be one of the more frustrating errors to debug if it happens to you.

Once the system reboots, you'll be able to log in using any valid credentials for a domain user. As you experienced with the domain controller, you can enter the domain or computer name, followed by a slash, and then the user name to choose which user account to use. Thankfully, here you can always use `.\` to log in as the local computer. In this case, let's use our domain user account.

Once you log in, let's take a look at the **Computer Management** interface to see what changed about the users and groups on the system. If you open up the Administrators group, you'll notice that it now includes an entry for `CIS527\Domain Admins`, and likewise the Users group contains a new entry for `CIS527\Domain Users`. That means, by default, any user on the domain can now log on to the computer as a user, and anyone on the domain with administrative privileges can log on to any computer on the domain and gain administrator permissions there as well. It is very important to understand these default permissions, so that you can assign them accordingly. For example, in many organizations, you may want to immediately remove the Domain Users entry from the Users group, and add a smaller group instead. You probably don't need folks from the Accounting department logging on to systems in Human Resources, right?

That's really all there is to it! You've successfully set up a Windows Active Directory Domain and added your first client computer to it. The next few videos will walk you through the same process on Ubuntu with OpenLDAP.
