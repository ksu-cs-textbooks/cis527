---
title: "Assignment"
weight: 15
pre: "3. "
---

## Lab 2 - Configuration Management

### Generative Artificial Intelligence Policy

{{% notice color="orange" %}}

<div style="display: block">
<div style="float: left; padding-right: 10px">
<img src="/cis527/images/0/stoplight_yellow.png" height="120px">
</div>
<div>
{{% badge style="orange" %}}YELLOW: Limited GenAI Usage Allowed {{% /badge %}} For your lab assignments, you may make limited use of GenAI tools to help with answering questions or debugging issues. These tools may also be helpful to understand dense documentation or search for answers online, but you <b>must review all AI results for accuracy</b>! Your submitted and graded lab must be your own work done entirely by you.
</div>
</div>
<div style="clear: both"></div>

* **Citations Required:** Any usage of GenAI must be noted and cited directly in the work. 
* **No Direct AI Results:** For this assignment, you **may not** include the GenAI results directly in your submission - this includes configuration files. You must write them yourself and adapt them to your specific setup, not just copy them from AI output. 
* **Understand Your Work:** You may be asked to explain your work in detail as part of this project. Failure to do so may be considered a violation of this policy.
* **Policy Violations:** Violations may result in a grade of 0 for the assignment and other sanctions approved through the K-State Honor Council.

{{% /notice %}}

### Instructions

Create two different **Puppet Manifest Files** that meet the specifications below. Each one will be applied to a newly installed virtual machine of the appropriate operating system configured as described in Task 0. The best way to accomplish this is to treat this assignment like a checklist and check things off as you complete them.

If you have any questions about these items or are unsure what they mean, please contact the instructor. Remember that part of being a system administrator (and a software developer in general) is working within vague specifications to provide what your client is requesting, so eliciting additional information is a very necessary skill.

{{% notice note %}}
_To be more blunt - this specification may be purposefully designed to be vague, and it is your responsibility to ask questions about any vagaries you find. Once you begin the grading process, you cannot go back and change things, so be sure that your machines meet the expected specification regardless of what is written here. --Russ_
{{% /notice %}}

Also, to complete many of these items, you may need to refer to additional materials and references not included in this document. System administrators must learn how to make use of available resources, so this is a good first step toward that. Of course, there's always [Google](http://www.google.com)!

#### Time Expectation

This lab may take anywhere from **1 - 6 hours** to complete, depending on your previous experience working with these tools and the speed of the hardware you are using.

{{% notice tip %}}
**Testing Manifest Files** - When testing these manifest files, there is a three step process. First, **apply** the manifest, then **reboot**, then **apply again**. This is because any changes made to group memberships are not applied until after a user logs back in or the system reboots. So, you may get permission issues when creating files or assigning permissions due to incorrect group memberships. Ideally, those permission errors should be eliminated after a reboot. There is no good fix for this in Puppet itself, since it is an operating system issue. Therefore, this is the process that you should use, and it is the process that will be used when your manifest files are graded. Basically, if you get no errors after a reboot, you should be fine!
{{% /notice %}}

---

### Task 0: Create New Virtual Machines & Snapshots

Create new Windows 11 and Ubuntu 26.04 virtual machines for this lab. When creating the virtual machines and installing the operating system, use the same information from Lab 1. You should create the `cis527` account during installation. 

**DO NOT PERFORM ANY ADDITIONAL CONFIGURATION AFTER THE INSTALLATION IS COMPLETE EXCEPT WHAT IS LISTED BELOW!**

After installing the operating system, install **ONLY** the following software:

* **OpenVox Agent 8**
  - Windows: Download and install the latest OpenVox Agent 8 from [OpenVox Downloads](https://downloads.voxpupuli.org/windows/openvox8/). Look for the file `openvox-agent-<version>-x64.msi` that is most recent. 
  - Ubuntu: See the video later in this module for instructions to install Puppet. These instructions are also summarized in the [Installing OpenVox Agent: Linux](https://docs.openvoxproject.org/openvox/latest/install_linux.html) guide.
    - Recall that Ubuntu 26.04 is codenamed "Resolute Raccoon", so use the url `https://apt.voxpupuli.org/openvox8-release-ubuntu26.04.deb` to get the correct version on Ubuntu in the first step. 
    - Follow the instructions in the video later in this lab to add Puppet to the `sudo` path. The path for OpenVox is the same as Puppet.

{{% notice note "OpenVox vs. Puppet" %}}

In 2025, Puppet moved to a different licensing model. Because of that, access to some of their software and tools became much more difficult. OpenVox is an open source fork of Puppet that aims to be 100% compatible with Puppet itself. So, we'll be building upon Puppet's language and framework, but using OpenVox as our actual agent tool. 

{{% /notice %}}

* **VMware Tools** (Windows) and either `open-vm-tools-desktop` or **VMware Tools** (Ubuntu)

* **All System Updates** (Windows & Ubuntu)

On the Windows virtual machine only, create a folder at `C:\install` and download the following installers. Do not change the name of the installers from the default name provided from the website. You may choose to do this step using the [download_file](https://forge.puppet.com/puppet/download_file) Puppet module instead.  

* [Firefox](https://www.firefox.com/en-US/download/all/) (`Firefox Setup 153.0.3.exe` as of 8/27/2026)
* [Thunderbird](https://www.thunderbird.net/en-US/thunderbird/all/) (`Thunderbird Setup 153.0.2.exe` as of  8/27/2026)
* [Notepad++](https://notepad-plus-plus.org/downloads/) (`npp.8.9.7.Installer.x64.exe` as of  8/27/2026)

{{% notice note %}}
_I have listed sample names of the installers as of this writing, and these will be the ones that I use for testing; however, you may receive newer versions with slightly different names. That is fine. Just be sure that you don't get the default stub or web-only installers, which is what Firefox typically gives you unless you follow the links above. They will not work properly for this lab. --Russ_
{{% /notice %}}

Once you have your virtual machines configured, make a snapshot of each called **"Puppet Testing"** for your use. As you test your Puppet manifest files, you'll reset to this snapshot to undo any changes made by Puppet so you can test on a clean VM. The VMs used for grading will be configured as described here.

{{% notice warning %}}
When you reset back to a snapshot, any new or modified files on the VM will be lost. So, make sure you keep a backup of the latest version of your manifest files on your host machine! _You have been warned!_
{{% /notice %}}

---

### Task 1: Puppet Manifest File for Ubuntu

Create a Puppet Manifest File for Ubuntu 26.04 that defines the following configuration. This configuration is very similar to, but not exactly the same as, Lab 1, so read through it carefully. Assume that the machine you are applying the manifest file on is configured as described above in Task 0.

* **Users (Same as Lab 1)**
  - `adminaccount` | `AdminPassword123` (Administrator type or `sudo` group)
  - `normalaccount` | `NormalPassword123` (Normal type)
  - `guestaccount` | `GuestPassword123` (Normal type)
  - `evilaccount` | `EvilPassword123` (Normal type)
  - _Create groups as needed below_{{% notice note %}}
Makes sure you can actually log in as these users after creating them! Many students forget to check this step and lose points because the accounts are created, but don't actually allow users to log in.
{{% /notice %}}

* **Files & Permissions (Same as Lab 1)**
  * Create a folder `/cis527` (**at the root of the system, not in a user's home folder**). Any user may read or write to this folder, and it should be owned by `root:root` (user: `root`; group: `root`).
  * Within `/cis527`, create a folder for each user created during task 5 except for `cis527`, with the folder name matching the user's name. Make sure that each folder is owned by the user of the same name, and that that user has full permissions to its namesake folder.
  * Create a group named `admingroup` and set permissions on each folder using that group to allow both `cis527` and `adminaccount` to have full access to each folder created in `/cis527`. No other user should be able to access any other user's folder. 
  * In each subfolder of `/cis527`, create a text file. It should have the same owner and access permissions as the folder it is contained in. The name and contents of the text file are up to you. 
  * See [this screenshot](images/lab1-image2.png) for what these permissions may look like in Terminal. This was created using the command `ls -lR` in the Linux terminal. These screenshots are from an earlier version of this lab using different paths and usernames, but the permissions structure is the same.

* **Software (Same as Lab 1)**
  - Mozilla Firefox (`firefox`)
  - Mozilla Thunderbird (`thunderbird`)
  - Apache Web Server (`apache2`)
  - Synaptic Package Manager (`synaptic`)
  - GUFW Firewall Management Utility (`gufw`)
  - ClamAV (`clamav`)

* **Services** - Ensure the following services are running:
  - Apache Web Server
  - Clam AntiVirus' FreshClam Service {{% notice note %}}
_You will have to find the appropriate name for each service. --Russ_
{{% /notice %}}

---

### Task 2: Puppet Manifest File for Windows 11

Create a Puppet Manifest File for Windows 11 that defines the following configuration. This configuration is very similar to, but not exactly the same as, Lab 1, so read through it carefully. Assume that the machine you are applying the manifest file on is configured as described above in Task 0.

* **Users (Same as Lab 1)**
  - `AdminAccount` | `AdminPassword123` (Administrators & Users group)
  - `NormalAccount` | `NormalPassword123` (Users group)
  - `GuestAccount` | `GuestPassword123` (Guests group only)
  - `EvilAccount` | `EvilPassword123` (Users group)
  - _Create groups as needed below_{{% notice note %}}
Makes sure you can actually log in as these users after creating them! Many students forget to check this step and lose points because the accounts are created, but don't actually allow users to log in.
{{% /notice %}}

* **Files & Permissions (Same as Lab 1)**
  * Create the folder `C:\cis527`. It should be owned by the `cis527` account, but make sure all other users can read and write to that folder.
  * Within `C:\cis527`, create a folder for each user created during task 2 except for `cis527`, with the folder name matching the user's name. Make sure that each folder is owned by the user of the same name, and that that user has full permissions to its namesake folder.
  * Create a group named `AdminGroup` containing `cis527` and `AdminAccount`, and set permissions on `C:\cis527` for that group to have full access to each folder created in `C:\cis527`. No other user should be able to access any other user's folder. 
  * In each subfolder of `C:\cis527`, create a text file. It should have the same owner and access permissions as the folder it is contained in. The name and contents of the text file are up to you. 
  * **Don't remove the SYSTEM account or the built-in Administrator account's access from any of these files.** Usually this is as simple as not modifying their permissions from the defaults.
  * See [this screenshot](/images/lab1-image1.png) and [this screenshot](/images/lab1-image1a.png) for what these permissions should look like in PowerShell. This was created using the command `Get-ChildItem -Recurse | Get-Acl | Format-List` in PowerShell. These screenshots are from an earlier version of this lab using different paths and usernames, but the permissions structure is the same.

* **Software** - Install the latest version of the following software. The installation should be done **SILENTLY** without any user interaction required. In addition, Puppet should be able to detect if they are already installed, and not attempt to install them again if the manifest is run multiple times.
  - Mozilla Firefox
  - Mozilla Thunderbird
  - Notepad++ {{% notice note %}}
_You will need to research the appropriate options to give to the installer through Puppet for them to install silently. For this lab, you should not use any Windows package managers such as Chocolatey or Ninite. The installation files will be already downloaded and stored in `C:\install`. Also, you'll need to make sure your resource names exactly match the names of the packages after they are installed, or Puppet will attempt to reinstall them each time the manifest file is applied. --Russ_
{{% /notice %}}

* **Services** - Ensure the following services are running:
  - DHCP Client
  - DNS Client
  - Windows Update {{% notice note %}}
_You will have to find the appropriate name for each service. --Russ_
{{% /notice %}}

---

### Task 3: Upload to Canvas & Contact Instructor

{{% notice note %}}
Please add comments to your Puppet Manifest Files describing any Puppet Modules that must be installed prior to applying them.
{{% /notice %}}

Upload your completed Puppet Manifest Files to Canvas and then contact the instructor for grading. You may continue with the next module once grading has been completed. In general, this lab does not require interactive grading, but you are welcome to request a time if you'd prefer.
