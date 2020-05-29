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
_Most students in previous semesters have reported that **this lab is generally the most frustrating and time-consuming** to complete. I recommend setting aside ample amounts of time to work on this lab. This is especially true if the system you are running your VMs on is not very powerful, since running multiple VMs at the same time may slow things down significantly. However, if you find that you are going in circles and not getting it to work, that would be a great time to ask for help. --Russ_
{{% /notice %}}

---

### Task 0: Create 4 VMs

For this lab, you'll need the following VMs:

1. A **Windows 10** VM. You may reuse your existing Windows 10 VM from a previous lab.
2. A **Windows Server 2019 Standard (Updated Sept 2019)** (or newer) VM. See **Task 1** below for configuration details.
3. An **Ubuntu 20.04** VM labelled **CLIENT**. This should be the existing **CLIENT** VM from Lab 3.
4. An **Ubuntu 20.04** VM labelled **SERVER**. _You have three options to create this VM:_
   * You can create a copy of your existing **CLIENT** VM from Lab 3, which does not have DHCP and DNS servers installed. Follow the instructions in the Lab 3 assignment to create a copy of that VM. In this case, you'll need to reconfigure the VMware NAT network to handle DHCP duties. Make sure you label this copy **SERVER** in VMWare. _This is generally the option that is simplest, and causes the least headaches._
   * You may continue to use your exiting **SERVER** VM from Lab 3, with DHCP and DNS servers installed. You may choose to continue to use this server as your primary DNS and DHCP server for your VM network, which would truly mimic what an enterprise network would be like. Remember that you'll need to have this VM running at all times to provide those services to other systems on your network. You may also choose instead to disable them and reconfigure the VMware NAT network to handle DHCP duties. Either approach is fine. _This option is generally a bit closer to an actual enterprise scenario, but can also cause many headaches, especially if your system doesn't have enough power to run several VMs simultaneously._
   * You may create a new Ubuntu 20.04 VM from scratch, label it **SERVER**, and configure it as defined either in Lab 1 or using the Puppet manifest files from Lab 2. _This is effectively the same as copying your **CLIENT** VM from Lab 3, but you get additional practice installing and configuring an Ubuntu VM, I guess._

{{% notice warning %}}
Before starting this lab, make a **snapshot** in each VM labelled "Before Lab 4" that you can restore to later if you have any issues. In addition, Task 6 below will ask you to restore to a snapshot in at least one VM before starting that step.
{{% /notice %}}

---

### Task 1: Install Windows Server 2019 Standard

Create a new virtual machine for **Windows Server 2019 Standard** using the "Windows Server 2019 Standard (Updated Sept 2019)" installation media (you may choose a newer option if available, but this lab was tested on that specific version). You can download the installation files and obtain a product key from the [Microsoft Azure Student Portal](https://support.cs.ksu.edu/CISDocs/wiki/FAQ#MSDNAA) discussed in Module 1. 

{{% notice tip %}}
For this system, I recommend giving the VM ample resources, usually at least 2 GB RAM and multiple processor cores if you can spare them. You may need to adjust the VM settings as needed to balance the performance of this VM against the available resources on your system. You may also have to choose "Windows Server 2016" as the operating system type in VMWare, as Windows Server 2019 may not be listed. 
{{% /notice %}}

When installing the operating system, configure it as specified below:

* Make sure you choose the **Desktop Experience** option when installing, unless you want a real challenge! It is possible to perform these steps without a GUI, but it is _much_ more difficult.
* **Computer Name:** `cis527d-<your eID>` (example: `cis527d-russfeld`)
* **Passwords:** Use `cis527_windows` as the password for the built-in Administrator account
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

1. First, set a static IP address on your Windows Server VM. Use the IP address ending in `42` that was reserved for this use in Lab 3. For the static DNS entries, use that same IP address or the localhost IP address (`127.0.0.1`) as the first entry, and then use the IP address of your DNS server (either your Ubuntu Server from Lab 3 or VMware's default gateway address, whichever option you are using) as the second DNS entry. In this way, the server will use itself as a DNS server first, and if that fails then it will use the other server. This is very important when dealing with Active Directory Domains, as the Domain Controller is also a DNS server.
2. Follow the instructions in the resources section below to install and configure the Active Directory Domain Services role on the server.
   * **Domain Name:** `ad.cis527<your eID>.cs.ksu.edu` (example: `ad.cis527russfeld.cs.ksu.edu`)
   * **Passwords:** Use `cis527_windows` for all passwords
3. Add a User Account to your Active Directory
   * Use your own eID for the username here, and `cis527_windows` as the password.

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

* [Join Windows 10 PC to a Domain](https://www.tenforums.com/tutorials/90045-join-windows-10-pc-domain.html) from Windows 10 Forums

---

### Task 4: Configure an OpenLDAP Server

Install OpenLDAP on your Ubuntu VM labelled **SERVER**. Follow the steps and configuration details below:

1. First, set a static IP address on your Ubuntu VM labelled **SERVER**, if it does not have one already. Use the IP address ending in `41` that was reserved for this use in Lab 3. For the static DNS entries, you should use one of the options discussed in Lab 3.
2. Set up and configure an OpenLDAP server, following the first part of the instructions in the guide linked in the resources section below.
   * **Domain Name:** `ldap.cis527<your eID>.cs.ksu.edu` (example: `ldap.cis527russfeld.cs.ksu.edu`)
   * **Base DN:** `dc=ldap,dc=cis527<your eID>,dc=cs,dc=ksu,dc=edu` (example: `dc=ldap,dc=cis527russfeld,dc=cs,dc=ksu,dc=edu`)
   * **Passwords:** Use `cis527_linux` for all passwords
   * You **DO NOT** have to perform the other steps in the guide to configure TLS at this point
3. Install phpLDAPadmin. See the video in this module for detailed instructions on how to install and configure phpLDAPadmin.
4. Add a User Account to your OpenLDAP Directory
   * Follow the instructions in the guide below to create `ou`s for `users`, `groups`, and create an `admin` group as well.
   * Use your own eID for the username, and `cis527_linux` as the password.
5. Configure the server to use TLS. You should follow the Ubuntu Server Guide to create and sign your own certificates. Make sure you use the correct domain name!
   * At the end of the process, copy the certificate at `/usr/local/share/ca-certificates/mycacert.crt` to the home directory of the `cis527` user for the next step.

Of course, you may need to modify your firewall configuration to allow incoming connections to the LDAP server!

#### Resources

* [How To Install and Configure OpenLDAP and phpLDAPadmin on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-openldap-and-phpldapadmin-on-ubuntu-16-04) from DigitalOcean (works for 18.04 and 20.04 as well)
* [Add Organizational Units, Groups and Users](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-a-basic-ldap-server-on-an-ubuntu-12-04-vps#add-organizational-units-groups-and-users) from DigitalOcean
* [LDAP & TLS](https://ubuntu.com/server/docs/service-ldap-with-tls) from the Ubuntu Server Guide

---

### Task 5: Configure Ubuntu to Authenticate via LDAP

On your Ubuntu VM labelled **CLIENT**, configure the system to authenticate against the OpenLDAP server created in Task 4.

* First, make sure that you can connect to the LDAP server using TLS. You can use `ldapwhoami -x -ZZ -h ldap.cis527<your eID>.cs.ksu.edu` and it should return `anonymous` if it works. 
* To test your SSSD configuration, use the command `getent passwd <username>` (example: `getent passwd russfeld`) and confirm that it returns an entry for your LDAP user.
* To log in as the LDAP user, use the `su <username>` command (example: `su russfeld`).
* Finally, **reboot the system**, and make sure you can log in graphically by choosing the "Not listed?" option on the login screen and entering your LDAP user's credentials.

#### Resources

* [SSSD](https://ubuntu.com/server/docs/service-sssd) on Ubuntu Server Guide (look for the "SSSD and LDAP" section)

---

### Task 6: Interoperability - Ubuntu Client on Windows Domain

1. On your Ubuntu VM labelled **CLIENT**, make a **snapshot** labelled "OpenLDAP" to save your configuration you performed for Task 5.
2. Open the Snapshot Manager (VM > Snapshot > Snapshot Manager) for that VM
3. Restore the "Before Lab 4" Snapshot. This should take you back to the state of this VM prior to setting it up as an OpenLDAP client.
4. Follow the instructions in the video in this module to join your Windows Active Directory Domain with your Ubuntu VM.
5. Make a **snapshot** labelled "ActiveDirectory" to save your configuration for this task. You can switch between snapshots to have this VM act as a client for either directory service.

#### Resources

* [Join in Active Directory Domain](https://www.server-world.info/en/note?os=Ubuntu_20.04&p=realmd) from Server-World
* [How to Join Ubuntu 18.04 / Debian 10 To Active Directory (AD) Domain](https://computingforgeeks.com/join-ubuntu-debian-to-active-directory-ad-domain/) from Computingforgeeks (works for 20.04)

---

### Task 7: Query Servers Using LDAPSearch

From your Ubuntu VM labelled **CLIENT**, use the `ldapsearch` command (in the `ldap-utils` package) to query your Active Directory and OpenLDAP servers. Take a **screenshot** of the output from each command.

Below are example commands from a working solution. You'll need to adapt them to match your environment. There are also sample screenshots of expected output.

* Active Directory Example [Screenshot](/images/lab4_win.png) (instructive, but using old data)

```bash
ldapsearch -LLL -H ldap://192.168.40.42:389 -b "dc=ad,dc=cis527russfeld,dc=cs,dc=ksu,dc=edu" -D "ad\Administrator" -w "cis527_windows"
```
* OpenLDAP Example [Screenshot](/images/lab4_ubu.png) (instructive, but using old data)

 ```bash
 ldapsearch -LLL -H ldap://192.168.40.41:389 -b "dc=ldap,dc=cis527russfeld,dc=cs,dc=ksu,dc=edu" -D "cn=admin,dc=ldap,dc=cis527russfeld,dc=cs,dc=ksu,dc=edu" -w "cis527_linux"
 ```   

{{% notice tip%}}
_You'll be asked to perform each of these commands as part of the grading process, but the screenshots provide good insurance in case you aren't able to get them to work --Russ_
{{% /notice %}}

---

### Task 8: Make Snapshots

In each of the virtual machines created above, create a snapshot labelled "Lab 4 Submit" before you submit the assignment. The grading process may require making changes to the VMs, so this gives you a restore point before grading starts. Also, you may have multiple Lab 4 snapshots on some VMs, so feel free to label them accordingly.

### Task 9: Schedule A Grading Time

Contact the instructor and schedule a time for interactive grading. You may continue with the next module once grading has been completed.
