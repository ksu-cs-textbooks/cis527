---
title: "Assignment"
weight: 15
pre: "3. "
---

### Lab 2 - Configuration Management

#### Instructions

Create two different **Puppet Manifest Files** that meet the specifications below. Each one will be applied to a newly installed virtual machine of the appropriate operating system configured as described in Task 0. The best way to accomplish this is to treat this assignment like a checklist and check things off as you complete them.

If you have any questions about these items or are unsure what they mean, please contact the instructor. Remember that part of being a system administrator (and a software developer in general) is working within vague specifications to provide what your client is requesting, so eliciting additional information is a very necessary skill.

{{% notice note %}}
_To be more blunt - this specification may be purposefully designed to be vague, and it is your responsibility to ask questions about any vagaries you find. Once you begin the grading process, you cannot go back and change things, so be sure that your machines meet the expected specification regardless of what is written here. --Russ_
{{% /notice %}}

Also, to complete many of these items, you may need to refer to additional materials and references not included in this document. System administrators must learn how to make use of available resources, so this is a good first step toward that. Of course, there's always [Google](http://www.google.com)!

#### Time Expectation

This lab may take anywhere from **1 - 6 hours** to complete, depending on your previous experience working with these tools and the speed of the hardware you are using.

---

### Task 0: Create New Virtual Machines & Snapshots

Create new Windows 10 and Ubuntu 18.04 virtual machines for this lab. When creating the virtual machines and installing the operating system, use the same information from Lab 1. You should create the cis527 account during installation. **DO NOT PERFORM ANY ADDITIONAL CONFIGURATION AFTER THE INSTALLATION IS COMPLETE EXCEPT WHAT IS LISTED BELOW!**

After installing the operating system, install **ONLY** the following software:

* Puppet Agent ([Windows](https://downloads.puppetlabs.com/windows/puppet5/) & Ubuntu)
* VMware Tools (Windows) and either `open-vm-tools-desktop` or VMware Tools (Ubuntu)
* All System Updates (Windows & Ubuntu)

On the Windows virtual machine only, create a folder at `C:\installers` and download the following installers. Do not change the name of the installers from the default name provided from the website. You may choose to do this step using the [download_file](https://forge.puppet.com/puppet/download_file) Puppet module instead.  

* [Firefox](https://www.mozilla.org/en-US/firefox/all/) (`Firefox Setup 61.0.2.exe` as of 8/31/2018)
* [Thunderbird](https://www.thunderbird.net/en-US/thunderbird/all/) (`Thunderbird Setup 60.0.exe` as of 8/31/2018)
* [Notepad++](https://notepad-plus-plus.org/download/) (`npp.7.5.8.Installer.exe` as of 8/31/2018)

{{% notice note %}}
_I have listed sample names of the installers as of this writing; however, you may receive newer versions with slightly different names. That is fine. Just be sure that you don't get the default stub or web-only installers, which is what Firefox typically gives you unless you follow the links below. They will not work properly for this lab. --Russ_
{{% /notice %}}

Once you have your Virtual Machines configured, make a snapshot of each called "Puppet Testing" for your use. As you test your Puppet manifest files, you'll reset to this snapshot to undo any changes made by Puppet so you can test on a clean VM. The VMs used for grading will be configured as described here.

{{% notice warning %}}
When you reset back to a snapshot, any new or modified files on the VM will be lost. So, make sure you keep a backup of the latest version of your manifest files on your host machine!
{{% /notice %}}

---

### Task 1: Puppet Manifest File for Ubuntu

Create a Puppet Manifest File for Ubuntu 18.04 that defines the following configuration. This configuration is very similar to, but not exactly the same as, Lab 1, so read through it carefully. Assume that the machine you are applying the manifest file on is configured as described above in Task 0.

* **Users (Same as Lab 1)**
  - AdminUser / AdminUser123 (Administrator type or sudo group)
  - NormalUser / NormalUser123 (Normal type)
  - GuestUser / GuestUser123 (Normal type)
  - EvilUser / EvilUser123 (Normal type)
  - _Create groups as needed below_
* **Files & Permissions (Same as Lab 1)**
  - Create a folder `/files` (at the root of the system, not in a user's home folder). Any user may read or write to this folder, and it should be owned by `root:root` (user: root; group: root).
  - Within `/files`, create a folder for each user created during task 5 except for cis527, with the folder name matching the user's name.
  - Make sure that each folder is owned by the user of the same name, and that that user has full permissions to its namesake folder.
  - Create a group and set permissions on each folder using that group to allow both cis527 and AdminUser to have full access to each folder created in /files.
  - No other user should be able to access any other user's folder. For example, EvilUser cannot access GuestUser's folder, but AdminUser and cis527 can, as well as GuestUser, who is also the owner of its own folder.
  - In each subfolder of `/files`, create a text file. It should have the same access permissions as the folder it is contained in. The name and contents of the text file are up to you.
  - See [this screenshot](/images/lab1-image2.png) for what these permissions may look like in Terminal.
* **Software (Same as Lab 1)**
  - Mozilla Firefox (`firefox`)
  - Mozilla Thunderbird (`thunderbird`)
  - Apache Web Server (`apache2`)
  - Synaptic Package Manager (`synaptic`)
  - GUFW Firewall Management Utility (`gufw`)
  - Conky (`conky`)
  - ClamAV (`clamav`)
* **Services** - Ensure the following services are running:
  - Apache Web Server
  - Clam AntiVirus' FreshClam Service
{{% notice note %}}
_You will have to find the appropriate name for each service. --Russ_
{{% /notice %}}

---

### Task 2: Puppet Manifest File for Windows 10

Create a Puppet Manifest File for Windows 10 that defines the following configuration. This configuration is very similar to, but not exactly the same as, Lab 1, so read through it carefully. Assume that the machine you are applying the manifest file on is configured as described above in Task 0.

* **Users (Same as Lab 1)**
  - AdminUser / AdminUser123 (Administrators & Users group)
  - NormalUser / NormalUser123 (Users group)
  - GuestUser / GuestUser123 (Guests group only)
  - EvilUser / EvilUser123 (Users group)
  - _Create groups as needed below_
* **Files & Permissions (Same as Lab 1)**
  - Create the folder `C:\files`. It should be owned by the cis527 account, but make sure all other users can read and write to that folder.
  - Within `C:\files`, create a folder for each user created during task 2 except for cis527, with the folder name matching the user's name.
  - Make sure that each folder is owned by the user of the same name, and that that user has full permissions to its namesake folder.
  - Create a group containing cis527 and AdminUser, and set permissions on `C:\files` for that group to have full access to each folder created in `C:\files`.
  - No other user should be able to access any other user's folder. For example, EvilUser cannot access GuestUser's folder, but AdminUser and cis527 can, as well as GuestUser, who is also the owner of its own folder.
  - In each subfolder of `C:\files`, create a text file. It should have the same access permissions as the folder it is contained in. The name and contents of the text file are up to you.
  - **Don't remove the SYSTEM account or the built-in Administrator account's access from any of these files.** Usually this is as simple as not modifying their permissions from the defaults.
  - See [this screenshot](/images/lab1-image1.png) for what these permissions may look like in PowerShell.
* **Software** - Install the latest version of the following software. The installation should be done SILENTLY without any user interaction required. In addition, Puppet should be able to detect if they are already installed, and not attempt to install them again.
  - Mozilla Firefox
  - Mozilla Thunderbird
  - Notepad++
{{% notice note %}}
_You will need to research the appropriate options to give to the installer through Puppet for them to install silently. For this lab, you should not use any Windows package managers such as Chocolatey or Ninite. Also, you'll need to make sure your resource names exactly match the names of the packages after they are installed, or Puppet will attempt to reinstall them each time the manifest file is applied. --Russ_
{{% /notice %}}
* **Services** - Ensure the following services are running:
  - DHCP Client
  - DNS Client
  - Windows Update
{{% notice note %}}
_You will have to find the appropriate name for each service. --Russ_
{{% /notice %}}

---

### Task 3 - Upload to Canvas & Contact Instructor

{{% notice note %}}
Please add comments to your Puppet Manifest Files describing any Puppet Modules that must be installed prior to applying them.
{{% /notice %}}

Upload your completed Puppet Manifest Files to Canvas and then contact the instructor for grading. You may continue with the next module once grading has been completed. In general, this lab does not require interactive grading, but you are welcome to request a time if you'd prefer.
