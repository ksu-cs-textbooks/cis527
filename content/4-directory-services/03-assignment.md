---
title: "Assignment"
weight: 15
pre: "3. "
---

### Lab 4 - Directory Services

#### Instructions

Create **four** virtual machines meeting the specifications given below. The best way to accomplish this is to treat this assignment like a checklist and check things off as you complete them.

If you have any questions about these items or are unsure what they mean, please contact the instructor. Remember that part of being a system administrator (and a software developer in general) is working within vague specifications to provide what your client is requesting, so eliciting additional information is a very necessary skill.

{{% notice note %}}
_To be more blunt - this specification may be purposefully designed to be vague, and it is your responsibility to ask questions about any vagaries you find. Once you begin the grading process, you cannot go back and change things, so be sure that your machines meet the expected specification regardless of what is written here. --Russ_
{{% /notice %}}

Also, to complete many of these items, you may need to refer to additional materials and references not included in this document. System administrators must learn how to make use of available resources, so this is a good first step toward that. Of course, there's always [Google](http://www.google.com)!

#### Time Expectation

This lab may take anywhere from **1 - 6 hours** to complete, depending on your previous experience working with these tools and the speed of the hardware you are using. Installing virtual machines and operating systems is very time-consuming the first time through the process, but it will be much more familiar by the end of this course.

{{% notice warning %}}
_Most students in previous semesters have reported that this lab is generally the most frustrating and time-consuming to complete. I recommend setting aside ample amounts of time to work on this lab. However, if you find that you are going in circles and not getting it to work, that would be a great time to ask for help. --Russ_
{{% /notice %}}

---

### Task 0: Create 4 VMs

For this lab, you'll need the following VMs:

1. A Windows 10 VM. You may reuse your existing Windows 10 VM from a previous lab.
2. A Windows Server 2016 Standard VM. See **Task 1** below for configuration details.
3. An Ubuntu 18.04 VM labelled **Client**. This should be the existing client VM from Lab 3.
4. An Ubuntu 18.04 VM labelled **Server**. You have two options:
  * You can create a copy of your existing **Client** from Lab 3, which does not have DHCP and DNS servers installed. Follow the instructions in the Lab 3 assignment to create a copy of that VM. In this case, you'll need to reconfigure the VMWare NAT network to handle DHCP duties. _This is generally the option that is simplest, and causes the least headaches._
  * You may continue to use your exiting **Server** from Lab 3, with DHCP and DNS servers installed. You may choose to continue to use this server as your primary DNS and DHCP server for your VM network, which would truly mimic what an enterprise network would be like. Remember that you'll need to have this VM running at all times to provide those services to other systems on your network. You may also choose instead to disable them and reconfigure the VMWare NAT network to handle DHCP duties. Either approach is fine. _This option is generally a bit closer to an actual enterprise scenario, but can also cause many headaches, especially if your system doesn't have enough power to run several VMs simultaneously._

---

### Task 1: Install Windows Server 2016 Standard

Create a new virtual machine for **Windows Server 2016 Standard**. You can download the installation files and obtain a product key from the [Microsoft Imagine Web Store](https://support.cs.ksu.edu/CISDocs/wiki/FAQ#MSDNAA) discussed in Module 1. For this system, I recommend giving the VM ample resources, usually at least 2 GB RAM and multiple processor cores if you can spare them. You may need to adjust the VM settings as needed to balance the performance of this VM against the available resources on your system.

When installing the operating system, configure it as specified below:

* **Computer Name:** CIS527D-\<your eID\> (example: CIS527D-russfeld)
* **Primary User Account:** cis527 / `cis527_windows` (Administrators & Users group)
* **Install Software**
  - [VMWare Tools](https://docs.vmware.com/en/VMware-Workstation-Pro/12.0/com.vmware.ws.using.doc/GUID-391BE4BF-89A9-4DC3-85E7-3D45F5124BC7.html)
  - [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/new/) (_you'll thank me later_)
* **Install Windows Updates:** Run Windows Update and reboot as necessary until all available updates are installed.
* **Automatic Updates:** Make sure the system is set to download and install security updates automatically.

---

### Task 2: Configure an Active Directory Domain Controller

Configure your Windows Server as an Active Directory Domain Controller. Follow the steps and configuration details below:

1. First, set a static IP address on your Windows Server VM. Use the IP address ending in `42` that was reserved for this use in Lab 3. For the static DNS entries, use that same IP address or the localhost IP address `127.0.0.1` as the first entry, and then the IP address of your DHCP server (either your Ubuntu Server from Lab 3 or VMWare's default gateway, whichever option you are using) as the second. In this way, the server will use itself as a DNS server first, and if that fails then it will use the other server. This is very important when dealing with Active Directory Domains, as the Domain Controller is also a DNS server.
2. Follow the instructions in the resources section below to install and configure the Active Directory Domain Services role on the server.
  * **Domain Name:** cis527\<your eID\>.local (example: cis527russfeld.local)
  * **Passwords:** Use `cis527_windows` for all passwords
3. Add a User Account to your Active Directory
  * Use your own eID for the username, and `cis527_windows` as the password.

#### Resources

* [Step-By-Step: Setting Up Active Directory in Windows Server 2016](https://blogs.technet.microsoft.com/canitpro/2017/02/22/step-by-step-setting-up-active-directory-in-windows-server-2016/) from Microsoft
* [Add User Accounts on Active Directory](https://www.server-world.info/en/note?os=Windows_Server_2016&p=active_directory&f=3) from Server-World

---

### Task 3: Join the Domain with Windows 10

Join your Windows 10 VM to the Active Directory Domain created in Task 2. Follow the steps and configuration details below:

1. First, set static DNS entries on your Windows 10 VM. You **SHOULD NOT** set a static IP, just static DNS entries. Use the Windows Server IP address ending in `42` as the first entry, and the second entry should be the same one used on the server earlier (either your Ubuntu Server from Lab 3 or VMWare's default gateway, whichever option you are using).
2. Join the system to the domain, following the instructions linked in the resources section below.
3. Once the system reboots, you should be able to log in using the user account you created in Task 2.

#### Resources

* [How to Join a Windows 10 PC to a Domain](https://www.groovypost.com/howto/join-a-windows-10-client-domain/) from groovyPost

---

### Task 4: Configure an OpenLDAP Server

Install OpenLDAP on your Ubuntu VM labelled **Server**. Follow the steps and configuration details below:

1. First, set a static IP address on your Ubuntu VM labelled **Server**, if it does not have one already. Use the IP address ending in `41` that was reserved for this use in Lab 3. For the static DNS entries, you should use one of the options discussed in Lab 3.
2. Set up and configure an OpenLDAP server and phpLDAPadmin on this system, following the instructions in the guide linked in the resources section below.
  * **Domain Name:** cis527\<your eID\>.local (example: cis527russfeld.local)
  * **Base DN:** `dc=cis527\<your eID\>,dc=local` (example: `dc=cis527russfeld,dc=local`)
  * **Passwords:** Use `cis527_linux` for all passwords
  * You **DO NOT** have to perform the last step in this guide, which involves configuring StartTLS Encryption.
3. Add a User Account to your Active Directory
  * Follow the instructions in the guide below to create `ou`s for `users`, `groups`, and create an `admin` group as well.
  * Use your own eID for the username, and `cis527_linux` as the password.

#### Resources

* [How To Install and Configure OpenLDAP and phpLDAPadmin on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-openldap-and-phpldapadmin-on-ubuntu-16-04) from DigitalOcean (works for 18.04 as well)
* [Add Organizational Units, Groups and Users](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-a-basic-ldap-server-on-an-ubuntu-12-04-vps#add-organizational-units-groups-and-users) from DigitalOcean

---

### Task 5: Configure Ubuntu to Authenticate via LDAP

On your Ubuntu VM labelled **Client**, configure the system to authenticate against the OpenLDAP server created in Task 4.

* To test your configuration, use the command `getent passwd` and confirm that you can see your eID in that list.
* To log in as the LDAP user, use the `su <username>` command (example: `su russfeld`).

#### Resources

* [Configure LDAP Client on Ubuntu 16.04 / Debian 8](https://www.itzgeek.com/how-tos/linux/ubuntu-how-tos/configure-ldap-client-on-ubuntu-16-04-debian-8.html) on IT'z Geek (should work on 18.04 as well)
* [Configure LDAP Client](https://www.server-world.info/en/note?os=Ubuntu_18.04&p=openldap&f=3) from Server-World
* [OpenLDAP Server](https://help.ubuntu.com/lts/serverguide/openldap-server.html.en) on Ubuntu Server Guide (look for the LDAP Authentication section)
* [How to Configure Ubuntu as an LDAP Client](https://askubuntu.com/questions/127389/how-to-configure-ubuntu-as-an-ldap-client) from AskUbuntu (possible solution to graphical login)

---

### Task 6: Query Servers Using LDAPSearch

From your Ubuntu VM labelled **Client**, use the `ldapsearch` command (in the `ldap-utils` package) to query your Active Directory and OpenLDAP servers. Take a **screenshot** of the output from each command.

Below are example commands from a working solution. You'll need to adapt them to match your environment. There are also sample screenshots of expected output.

* Active Directory Example: `ldapsearch -LLL -H ldap://192.168.40.42:389 -b "dc=cis527russfeld,dc=local" -D "cis527russfeld\Administrator" -w "cis527_windows"`
  * [Screenshot](/images/lab4_win.png)
* OpenLDAP Example: `ldapsearch -LLL -H ldap://192.168.40.41:389 -b "dc=cis527russfeld,dc=local" -D "cn=admin,dc=cis527russfeld,dc=local" -w "cis527_linux"`
  * [Screenshot](/images/lab4_ubu.png)
