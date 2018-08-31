---
title: "Windows 10 Security & Networking"
weight: 55
pre: "11. "
---

{{< youtube zu7tQdw27z4 >}}

#### Resources

* [Slides]({{< relref "/1-secure-workstations/11-windows-security-networking-slides.md" >}})
* [Adjust Windows 10 Firewall Rules & Settings](https://www.online-tech-tips.com/windows-10/adjust-windows-10-firewall-settings/) from Online Tech Tips
* [Configuring Virtual Network Adapter Settings](https://docs.vmware.com/en/VMware-Workstation-Pro/12.0/com.vmware.ws.using.doc/GUID-C82DCB68-2EFA-460A-A765-37225883337D.html) from VMWare
* [Using the Virtual Network Editor](https://docs.vmware.com/en/VMware-Workstation-Pro/12.0/com.vmware.ws.using.doc/GUID-AC956B17-30BA-45F7-9A39-DCCB96B0A713.html) from VMWare

#### Video Script

In this last video on Windows 10, we'll discuss some important security and networking details needed to finish getting your VMs set up and configured properly.

First, let's talk about security. Whenever you install a new operating system, there are 4 major steps you should always perform before doing just about anything else on the system. Those steps are:

1. **Configure User Accounts & Passwords** - at least get your administrator and standard account set up. You can add more users later, or you may add it to an Active Directory Domain for user accounts.
1. **Configure the Firewall** - Windows 10 has the firewall enabled by default, but you should always confirm that your firewall is active before accessing the internet. On older, unpatched versions of Windows, researchers were able to demonstrate that the system can be compromised in as little as 5 minutes just by connecting it to the internet without any additional security or steps taken.
2. **Install Antivirus Software** - All computers should still run some form of antivirus software. Windows comes with Windows Defender installed by default, and it will suffice as a basic form of antivirus protection. On a production system, I recommend installing a professional antivirus solution if possible.
1. **Install All System Updates** - You should also install all available system updates for your operating system. This makes sure you have patches against the latest known flaws and attacks. Windows will generally do so for you automatically, but you can check for updates manually through the Windows Update.

Let's take a quick look at the Windows Firewall, since you'll need to allow an application through the firewall. You can find it by searching for "firewall" on the Start Menu. Lab 1 directs you to install the Internet Information Services (IIS) web server. You'll need to allow it through the firewall somehow. I won't show you how in this video, but I encourage you to review the links in the resources section below the video for documentation showing how to accomplish this task. There are several ways to do it.

To test your firewall configuration, you can use your Ubuntu virtual machine created as part of Lab 1. First, make sure they are both on the same network segment in VMWare by looking at the hardware configuration for each virtual machine. Then, you'll need to get the IP address of the Windows computer. There are several ways to do this, but one of the simplest is to go to the Network Settings by clicking the networking icon in the system tray, near the clock, then choosing the Ethernet adapter. Here you'll find the IPv4 address, usually in form of four numbers separated by decimal points. We'll spend most of Module 3 discussing networking, so I won't go into too much detail here.

Once you have that IP address, switch to your Ubuntu virtual machine, and open up the Firefox web browser. At the top in the address bar, simply input the IP address and press enter. If everything works correctly, you should be presented with the default IIS screen as seen here. If not, you'll need to do some debugging to figure out what is missing.

With that, you should now have all the information you need to finish the Windows portion of Lab 1. If you have issues, please feel free to post in the course discussion forums or chat with me. Good luck!
