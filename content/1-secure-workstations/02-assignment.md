---
title: "Assignment"
weight: 10
pre: "2. "
---
{{% notice warning %}}
This is the assignment page for Lab 1. It is placed before the rest of the module's content so you may begin working on it as you review the content. Click **Next** below to continue to the rest of the module.
{{% /notice %}}

### Lab 1 - Secure Workstations

#### Instructions

Create two virtual machines meeting the specifications given below. The best way to accomplish this is to treat this assignment like a checklist and check things off as you complete them.

If you have any questions about these items or are unsure what they mean, please contact the instructor. Remember that part of being a system administrator (and a software developer in general) is working within vague specifications to provide what your client is requesting, so eliciting additional information is a very necessary skill.

{{% notice note %}}
_To be more blunt - this specification may be purposefully designed to be vague, and it is your responsibility to ask questions about any vagaries you find. Once you begin the grading process, you cannot go back and change things, so be sure that your machines meet the expected specification regardless of what is written here. --Russ_
{{% /notice %}}

Also, to complete many of these items, you may need to refer to additional materials and references not included in this document. System administrators must learn how to make use of available resources, so this is a good first step toward that. Of course, there's always [Google](http://www.google.com)!

#### Time Expectation

This lab may take anywhere from **1 - 6 hours** to complete, depending on your previous experience working with these tools and the speed of the hardware you are using. Installing virtual machines and operating systems is very time-consuming the first time through the process, but it will be much more familiar by the end of this course.

#### Software

This lab is written with the expectation that most students will be using **VMware Workstation** or **VMware Fusion** to complete the assignment. That software is available free of charge on the [VMware Store](https://support.cs.ksu.edu/CISDocs/wiki/FAQ#VMWare) open to all K-State CS students, and it is highly recommended for students who are new to working with virtual machines, since most of the assignments in this class are tailored to the use of that platform.

If you are using another virtualization platform, you may have to adapt these instructions to fit. If you are unsure about any specification and how it applies to your setup, please contact the instructor.

You will also need installation media for the following operating systems:
* **Windows 10 Version 1903** - See the [Azure Dev Tools](https://support.cs.ksu.edu/CISDocs/wiki/FAQ#MSDNAA) page on the CS Support Wiki for instructions.
  * File Name: `en_windows_10_consumer_editions_version_1903_x64_dvd_b980e68c.iso`
  * MD5 Hash: `8ba0e81b276d9052e8538deb0cf6c7d0`
  * _Your file may vary as Microsoft constantly updates these installers._
* **Ubuntu 20.04 LTS** - Download from [Ubuntu](https://ubuntu.com/download) or the [K-State CS Mirror](http://mirror.cs.ksu.edu/ubuntu-releases/focal/)
  * File Name: `ubuntu-20.04-desktop-amd64.iso`
  * MD5 Hash: `ea28c4fd933be55f9f01a5fa9e868490`
  * _If a point release is avialble (ex: 20.04.1), feel free to us that version._

{{% notice note %}}
The original course materials were developed for Windows 10 Version 1803 and Ubuntu 18.04 LTS. Some course materials may still show the older versions. Students should use the software versions listed in bold above if at all possible. If not, please contact the instructor for alternative options. If you find any errors or issues using the updated versions of these systems, please post on Piazza.    
{{% /notice %}}

---

### Task 0: Install Virtualization Software

Install the virtualization software platform of your choice. It must support using Windows 10 and Ubuntu 20.04 as a guest OS. In general, you'll need the latest version of the software. 

**VMware Workstation** or **VMware Fusion** is recommended and available free of charge on the [VMware Store](https://support.cs.ksu.edu/CISDocs/wiki/FAQ#VMWare) open to all K-State CS students.

You may need to install the latest version available for download and then update it within the software to get to the absolute latest version that supports the latest guest OS versions.

---

### Task 1: Create a Windows 10 Virtual Machine

Create a new virtual machine for Windows 10. It should have 60 GB of storage available. If given the option, do not pre-allocate the storage, but do allow it to be separated into multiple files. This will make the VM easier to work with down the road. It should also have at least 2 GB of RAM. You may allocate more RAM if desired. You may also allocate additional CPU cores for better performance if desired. 

Install Windows 10 in that virtual machine to a single partition. You may use the express settings when configuring Windows. **Do not use a Microsoft account to sign in!** Instead, create a local (non-Microsoft) account as defined below. You may also be asked to set the computer name, which is given below.

{{% notice note %}}
Windows 10 Version 1903 has made it more difficult to create a local account when installing. See the video later in this module for instructions or refer to this guide from [How-To Geek](https://www.howtogeek.com/442792/how-to-create-a-local-account-while-setting-up-windows-10/)
{{% /notice %}}

### Task 2: Configure Windows 10

Configure the Windows 10 Virtual Machine as specified below.

* **Computer Name:** `cis527w-<your eID>` (example: `cis527w-russfeld`)
{{% notice info %}}
_This is very important, as it allows us to track your virtual machine on the K-State network in case something goes wrong in a later lab. By including both the class and your eID, support staff will know who to contact. A majority of students have missed this step in previous semesters, so don't forget! --Russ_
{{% /notice %}}
* **Primary User Account:** Username: `cis527` |  Password: `cis527_windows` (Member of Administrators & Users groups)
* **Other User Accounts:**
  - `AdminUser` | `AdminPassword123` (Administrators & Users group)
  - `NormalUser` | `NormalPassword123` (Users group)
  - `GuestUser` | `GuestPassword123` (Guests group only)
  - `EvilUser` | `EvilPassword123` (Users group)
* **Install Software**
  - [VMware Tools](https://kb.vmware.com/s/article/1014294)
  - [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/new/)
  - [Mozilla Thunderbird](https://www.thunderbird.net/en-US/)
  - [IIS Web Server](https://www.howtogeek.com/112455/how-to-install-iis-8-on-windows-8/)
  - [Notepad++](https://notepad-plus-plus.org/)
  - [BGInfo](https://docs.microsoft.com/en-us/sysinternals/downloads/bginfo) _Download the Bginfo.exe file and place it on the cis527 user's desktop. It does not have an installation program. Run it once to see what it does!_
  - Verify Windows Defender is running. It should be installed by default.
* **Configure Firewall**
  - Make sure Windows Firewall is enabled
  - Allow all incoming connections to port 80 (for IIS)
  {{% notice tip %}}
You can test this by accessing the Windows VM IP Address from Firefox running on your Ubuntu VM, provided they are on the same virtual network.
{{% /notice %}}
* **Install Windows Updates:** Run Windows Update and reboot as necessary until all available updates are installed.
* **Automatic Updates:** Make sure the system is set to download and install security updates automatically.

{{% notice note %}}
Even though you may have installed a particular version of Windows, such as 1903, you should run updates repeatedly until there are no more updates available. You may end up installing at least one major update rollup. 
{{% /notice %}}

### Task 3: Windows Files & Permissions

{{%notice warning %}}
_Read the whole task before you start! You have been warned. --Russ_
{{% /notice %}}

* Create the folder `C:\files`. It should be owned by the `cis527` account, but make sure all other users can read and write to that folder.
* Within `C:\files`, create a folder for each user created during task 2 except for `cis527`, with the folder name matching the user's name.
* Make sure that each folder is owned by the user of the same name, and that that user has full permissions to its namesake folder.
* - Create a group containing `cis527` and `AdminUser`, and set permissions on `C:\files` for that group to have full access to each folder created in `C:\files`.
{{% notice tip %}}
When you create a group and add a user to that group, it does not take effect until you reboot the computer.
{{% /notice %}}
* No other user should be able to access any other user's folder. For example, `EvilUser` cannot access `GuestUser`'s folder, but `AdminUser` and `cis527` can, as well as `GuestUser`, who is also the owner of its own folder.
* In each subfolder of `C:\files`, create a text file. It should have the same access permissions as the folder it is contained in. The name and contents of the text file are up to you.
{{% notice tip %}}
Use either the `cis527` or `AdminUser` account to create these files, then modify the owner and permissions as needed. Verify that they can only be accessed by the correct users by logging in as each user and seeing what can and can't be accessed by that user, or by using the permissions auditing tab. Many students neglect this step, leaving the file owner incorrect.
{{% /notice %}}
* **Don't remove the SYSTEM account or the built-in Administrator account's access from any of these files.** Usually this is as simple as not modifying their permissions from the defaults.
* See [this screenshot](/images/lab1-image1.png) and [this screenshot](/images/lab1-image1a.png) for what these permissions should look like in PowerShell.

---

### Task 4: Create an Ubuntu 20.04 Virtual Machine

Create a new virtual machine for Ubuntu 20.04 Desktop. It should have 30 GB of storage available. If given the option, do not pre-allocate the storage, but do allow it to be separated into multiple files. This will make the VM easier to work with down the road. It should also have at least 2 GB of RAM. You may allocate more RAM if desired. You may also allocate additional CPU cores for better performance if desired. 

{{% notice note %}}
_Ubuntu 20.04 seems to be really RAM hungry right now, so I recommend starting with 2 GB of RAM if you have 8 GB or more available on your system. The installer may freeze if you try to install with only 1 GB of RAM allocated. Once you have it installed, you may be able to reduce this at the expense of some performance if you are short on available RAM (as it will use swap space instead). In Ubuntu, swap should be enabled by default after you install it, but you can learn more about it and how to configure it [here](https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-20-04). When we get to Module 5 and discuss Ubuntu in the cloud, we'll come back to this and discuss the performance trade-offs in that scenario. --Russ_
{{% /notice %}}

Install Ubuntu 20.04 Desktop in that virtual machine to a single partition. You will be asked to create a user account and set the computer name. Use the information given below.

{{% notice tip %}}
The Ubuntu installation will sometimes hang when rebooting after installation in a VM. If that happens, wait about 30 seconds, then click **VM > Power > Restart Guest** in VMware (or similar) to force a restart. It should not harm the VM.
{{% /notice %}}

### Task 5: Configure Ubuntu 20.04

Configure the Ubuntu 20.04 Virtual Machine as specified below.

* **Computer Name:** `cis527u-<your eID>` (example: `cis527u-russfeld`)
{{% notice info %}}
_This is very important, as it allows us to track your virtual machine on the K-State network in case something goes wrong in a later lab. By including both the class and your eID, support staff will know who to contact. A majority of students have missed this step in previous semesters, so don't forget! --Russ_
{{% /notice %}}
* **Primary User Account:** Username: `cis527` | Password: `cis527_linux` (Account should have Administrator type or be in the `sudo` group)
* **Other User Accounts:**
  - `adminuser` | `AdminPassword123` (Administrator type or `sudo` group)
  - `normaluser` | `NormalPassword123` (Normal type)
  - `guestuser` | `GuestPassword123` (Normal type)
  - `eviluser` | `EvilPassword123` (Normal type)
* **Install Software**
  - Open VM Tools (`open-vm-tools-desktop`) (recommended) -OR- [VMware Tools](https://kb.vmware.com/s/article/1022525) (do not install both)
  - Mozilla Firefox (`firefox`)
  - Mozilla Thunderbird (`thunderbird`)
  - Apache Web Server (`apache2`)
  - Synaptic Package Manager (`synaptic`)
  - GUFW Firewall Management Utility (`gufw`)
  - Conky (`conky`)
  - ClamAV (`clamav`)
* **Configure Firewall**
  - Make sure Ubuntu Firewall (use `ufw`, not `iptables`) is enabled
  - Allow all incoming connections to port 80 (for Apache)
{{% notice tip %}}
You can test this by accessing the Ubuntu VM IP Address from Firefox on your Windows VM, provided they are on the same virtual network.
{{% /notice %}}
* **Install Updates:** Run system updates and reboot as necessary until all available updates are installed.
* **Automatic Updates:** Configure the system to download and install security updates automatically each day.

### Task 6: Ubuntu Files & Permissions

{{%notice warning %}}
_Read the whole task before you start! You have been warned. --Russ_
{{% /notice %}}

* Create a folder `/files` (**at the root of the system, not in a user's home folder**). Any user may read or write to this folder, and it should be owned by `root:root` (user: `root`; group: `root`).
* Within `/files`, create a folder for each user created during task 5 except for `cis527`, with the folder name matching the user's name.
* Make sure that each folder is owned by the user of the same name, and that that user has full permissions to its namesake folder.
* Create a group and set permissions on each folder using that group to allow both `cis527` and `AdminUser` to have full access to each folder created in /files.
{{% notice tip %}}
When you create a group and add a user to that group, it does not take effect until you reboot the computer.
{{% /notice %}}
* No other user should be able to access any other user's folder. For example, `EvilUser` cannot access `GuestUser`'s folder, but `AdminUser` and `cis527` can, as well as `GuestUser`, who is also the owner of its own folder.
* In each subfolder of `/files`, create a text file. It should have the same access permissions as the folder it is contained in. The name and contents of the text file are up to you.
{{% notice tip %}}
Use either the `cis527` or `AdminUser` account to create these files, then modify the owner, group, and permissions as needed. Verify that they can only be accessed by the correct users by logging in as each user and seeing what can and can't be accessed by that user, or by using the `su` command to become that user in the terminal. Many students neglect this step, leaving the file owner incorrect.
{{% /notice %}}
* See [this screenshot](/images/lab1-image2.png) for what these permissions may look like in Terminal.

---

### Task 7: Make Snapshots

For each of the virtual machines created above, create a snapshot labelled *Lab 1 Submit* in your virtualization software before you submit the assignment. The grading process may require making changes to the VMs, so this gives you a restore point before grading starts.

### Task 8: Schedule A Grading Time

Contact the instructor and schedule a time for interactive grading. You may continue with the next module once grading has been completed.