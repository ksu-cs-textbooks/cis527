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
3. An Ubuntu 18.04 VM labelled **CLIENT**. This should be the existing client VM from Lab 3.
4. An Ubuntu 18.04 VM labelled **SERVER**. You have two options:
  * You can create a copy of your existing **CLIENT** from Lab 3, which does not have DHCP and DNS servers installed. Follow the instructions in the Lab 3 assignment to create a copy of that VM. In this case, you'll need to reconfigure the VMware NAT network to handle DHCP duties. _This is generally the option that is simplest, and causes the least headaches._
  * You may continue to use your exiting **SERVER** from Lab 3, with DHCP and DNS servers installed. You may choose to continue to use this server as your primary DNS and DHCP server for your VM network, which would truly mimic what an enterprise network would be like. Remember that you'll need to have this VM running at all times to provide those services to other systems on your network. You may also choose instead to disable them and reconfigure the VMware NAT network to handle DHCP duties. Either approach is fine. _This option is generally a bit closer to an actual enterprise scenario, but can also cause many headaches, especially if your system doesn't have enough power to run several VMs simultaneously._

{{% notice warning %}}
Before starting this lab, make a **snapshot** in each VM labelled "Before Lab 4" that you can restore to later if you have any issues. In addition, Task 6 below will ask you to restore to a snapshot in at least one VM before starting that step.
{{% /notice %}}

---

### Task 1: Install Windows Server 2016 Standard

Create a new virtual machine for **Windows Server 2016 Standard**. You can download the installation files and obtain a product key from the [Microsoft Imagine Web Store](https://support.cs.ksu.edu/CISDocs/wiki/FAQ#MSDNAA) discussed in Module 1. For this system, I recommend giving the VM ample resources, usually at least 2 GB RAM and multiple processor cores if you can spare them. You may need to adjust the VM settings as needed to balance the performance of this VM against the available resources on your system.

When installing the operating system, configure it as specified below:

* Make sure you choose the **Desktop Experience** option when installing, unless you want a real challenge! It is possible to perform these steps without a GUI, but it is _much_ more difficult.
* **Computer Name:** CIS527D-\<your eID\> (example: CIS527D-russfeld)
* **Install Software**
  - [VMware Tools](https://docs.vmware.com/en/VMware-Workstation-Pro/12.0/com.vmware.ws.using.doc/GUID-391BE4BF-89A9-4DC3-85E7-3D45F5124BC7.html)
  - [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/new/) (_you'll thank me later_)
* **Install Windows Updates:** Run Windows Update and reboot as necessary until all available updates are installed.
* **Automatic Updates:** Make sure the system is set to download and install security updates automatically.

Make a **snapshot** of this VM once it is fully configured and updated. You can restore to this snapshot if you have issues installing Active Directory.

{{% notice tip %}}
You can use <kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>Insert</kbd> to send a <kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>Delete</kbd> to your VM in VMware without affecting your host OS.
{{% /notice %}}

---

### Task 2: Configure an Active Directory Domain Controller

Configure your Windows Server as an Active Directory Domain Controller. Follow the steps and configuration details below:

1. First, set a static IP address on your Windows Server VM. Use the IP address ending in `42` that was reserved for this use in Lab 3. For the static DNS entries, use that same IP address or the localhost IP address `127.0.0.1` as the first entry, and then the IP address of your DHCP server (either your Ubuntu Server from Lab 3 or VMware's default gateway, whichever option you are using) as the second. In this way, the server will use itself as a DNS server first, and if that fails then it will use the other server. This is very important when dealing with Active Directory Domains, as the Domain Controller is also a DNS server.
2. Follow the instructions in the resources section below to install and configure the Active Directory Domain Services role on the server.
  * **Domain Name:** ad\<username\>.cis527.cs.ksu.edu (example: `adrussfeld.cis527.cs.ksu.edu`)
  * **Passwords:** Use `cis527_windows` for all passwords
3. Add a User Account to your Active Directory
  * Use your own eID for the username, and `cis527_windows` as the password.

#### Resources

* [Step-By-Step: Setting Up Active Directory in Windows Server 2016](https://blogs.technet.microsoft.com/canitpro/2017/02/22/step-by-step-setting-up-active-directory-in-windows-server-2016/) from Microsoft
* [Add User Accounts on Active Directory](https://www.server-world.info/en/note?os=Windows_Server_2016&p=active_directory&f=3) from Server-World
* [AD DS Installation and Removal Wizard Page Descriptions](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/deploy/ad-ds-installation-and-removal-wizard-page-descriptions) from Microsoft

---

### Task 3: Join the Domain with Windows 10

Join your Windows 10 VM to the Active Directory Domain created in Task 2. Follow the steps and configuration details below:

1. First, set static DNS entries on your Windows 10 VM. You **SHOULD NOT** set a static IP, just static DNS entries. Use the Windows Server IP address ending in `42` as the first entry, and the second entry should be the same one used on the server earlier (either your Ubuntu Server from Lab 3 or VMware's default gateway, whichever option you are using).
2. Join the system to the domain, following the instructions linked in the resources section below.
3. Once the system reboots, you should be able to log in using the user account you created in Task 2.

#### Resources

* [How to Join a Windows 10 PC to a Domain](https://www.groovypost.com/howto/join-a-windows-10-client-domain/) from groovyPost

---

### Task 4: Configure an OpenLDAP Server

Install OpenLDAP on your Ubuntu VM labelled **SERVER**. Follow the steps and configuration details below:

1. First, set a static IP address on your Ubuntu VM labelled **SERVER**, if it does not have one already. Use the IP address ending in `41` that was reserved for this use in Lab 3. For the static DNS entries, you should use one of the options discussed in Lab 3.
2. Set up and configure an OpenLDAP server, following the first part of the instructions in the guide linked in the resources section below.
  * **Domain Name:** cis527\<your eID\>.local (example: cis527russfeld.local)
  * **Base DN:** `dc=cis527\<your eID\>,dc=local` (example: `dc=cis527russfeld,dc=local`)
  * **Passwords:** Use `cis527_linux` for all passwords
  * You **DO NOT** have to perform the other steps in the guide at this point
3. Install phpLDAPadmin from https://github.com/breisig/phpLDAPadmin. See the video in this module for detailed instructions on how to install and configure phpLDAPadmin.
4. Add a User Account to your Active Directory
  * Follow the instructions in the guide below to create `ou`s for `users`, `groups`, and create an `admin` group as well.
  * Use your own eID for the username, and `cis527_linux` as the password.

Of course, you may need to modify your firewall configuration to allow incoming connections to the LDAP server!

#### Resources

* [How To Install and Configure OpenLDAP and phpLDAPadmin on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-openldap-and-phpldapadmin-on-ubuntu-16-04) from DigitalOcean (works for 18.04 as well)
* [Add Organizational Units, Groups and Users](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-a-basic-ldap-server-on-an-ubuntu-12-04-vps#add-organizational-units-groups-and-users) from DigitalOcean

---

### Task 5: Configure Ubuntu to Authenticate via LDAP

On your Ubuntu VM labelled **CLIENT**, configure the system to authenticate against the OpenLDAP server created in Task 4.

* To test your configuration, use the command `getent passwd <username>` (example: `getent passwd russfeld`) and confirm that it returns an entry for your LDAP user.
* To log in as the LDAP user, use the `su <username>` command (example: `su russfeld`).
* Finally, reboot the system, and make sure you can log in graphically by choosing the "Not listed?" option on the login screen and entering your LDAP user's credentials.

#### Resources

* [Configure LDAP Client on Ubuntu 16.04 / Debian 8](https://www.itzgeek.com/how-tos/linux/ubuntu-how-tos/configure-ldap-client-on-ubuntu-16-04-debian-8.html) on ITz Geek (should work on 18.04 as well)
* [Configure LDAP Client](https://www.server-world.info/en/note?os=Ubuntu_18.04&p=openldap&f=3) from Server-World
* [OpenLDAP Server](https://help.ubuntu.com/lts/serverguide/openldap-server.html.en) on Ubuntu Server Guide (look for the LDAP Authentication section)

---

### Task 6: Interoperability

**!! COMPLETE ONE OF THE OPTIONS BELOW !!**

#### Task 6A: Ubuntu Client on Windows Domain

1. On your Ubuntu VM labelled **CLIENT**, make a **snapshot** labelled "OpenLDAP" to save your configuration you performed for Task 5.
2. Open the Snapshot Manager (VM > Snapshot > Snapshot Manager) for that VM
3. Restore the "Before Lab 4" Snapshot. This should take you back to the state of this VM prior to setting it up as an OpenLDAP client.
4. Follow the instructions in the video in this module to join your Windows Active Directory Domain with your Ubuntu VM.
5. Make a **snapshot** labelled "ActiveDirectory" to save your configuration for this task. You can switch between snapshots to have this VM act as a client for either directory service.

#### Task 6B: Windows Client on Ubuntu Domain

1. On your Ubuntu VM labelled **CLIENT**, make a **snapshot** labelled "OpenLDAP" to save your configuration you performed for Task 5.
2. Open the Snapshot Manager (VM > Snapshot > Snapshot Manager) for that VM
3. Restore the "Before Lab 4" Snapshot. This should take you back to the state of this VM prior to setting it up as an OpenLDAP client.
4. On your Windows 10 VM, make a **snapshot** labelled "ActiveDirectory" to save your configuration you performed for Task 3.
5. Open the Snapshot Manager (VM > Snapshot > Snapshot Manager) for that VM
6. Restore the "Before Lab 4" Snapshot. This should take you back to the state of this VM prior to adding it to your Active Directory Domain.
7. Follow the instructions in the video in this module to create a Samba Domain Controller on your Ubuntu VM labelled **CLIENT**, and then add your Windows 10 VM to that domain. For the realm, use `smb<username>.cis527.cs.ksu.edu`. (For example, mine would be `smbrussfeld.cis527.cs.ksu.edu`.)
8. On both of those VMs, make a **snapshot** labelled "Samba" to save your configuration for this task. You can switch between snapshots on these VMs for each configuration.

#### Resources

* [Join Ubuntu 18.04 to Active Directory](https://bitsofwater.com/2018/05/08/join-ubuntu-18-04-to-active-directory/) by Michael Waterman from Bits of Water
* [How to Configure Ubuntu Linux Server as a Domain Controller with Samba-tool](https://www.techrepublic.com/article/how-to-configure-ubuntu-linux-server-as-a-domain-controller-with-samba-tool/) by Jack Wallen on TechRepublic
* [Samba Not Starting on Ubuntu Server 16.10](https://unix.stackexchange.com/questions/341226/samba-not-starting-on-ubuntu-server-16-10) from StackExchange
* [How to Disable Systemd-resolved in Ubuntu](https://askubuntu.com/questions/907246/how-to-disable-systemd-resolved-in-ubuntu) from AskUbuntu

---

### Task 7: Query Servers Using LDAPSearch

From your Ubuntu VM labelled **CLIENT**, use the `ldapsearch` command (in the `ldap-utils` package) to query your Active Directory and OpenLDAP servers. Take a **screenshot** of the output from each command.

Below are example commands from a working solution. You'll need to adapt them to match your environment. There are also sample screenshots of expected output.

* Active Directory Example: `ldapsearch -LLL -H ldap://192.168.40.42:389 -b "dc=adrussfeld,dc=cis527,dc=cs,dc=ksu,dc=edu" -D "adrussfeld\Administrator" -w "cis527_windows"`
  * [Screenshot](/images/lab4_win.png)
* OpenLDAP Example: `ldapsearch -LLL -H ldap://192.168.40.41:389 -b "dc=cis527russfeld,dc=local" -D "cn=admin,dc=cis527russfeld,dc=local" -w "cis527_linux"`
  * [Screenshot](/images/lab4_ubu.png)

{{% notice tip%}}
_You'll present those 2 screenshots as part of the grading process for this lab, so I recommend storing them on the desktop of that VM so they are easy to find. --Russ_
{{% /notice %}}

---

### Task 8: Make Snapshots

In each of the virtual machines created above, create a snapshot labelled "Lab 4 Submit" before you submit the assignment. The grading process may require making changes to the VMs, so this gives you a restore point before grading starts. Also, you may have multiple Lab 4 snapshots on some VMs, so feel free to label them accordingly.

### Task 9: Schedule A Grading Time

Contact the instructor and schedule a time for interactive grading. You may continue with the next module once grading has been completed.
