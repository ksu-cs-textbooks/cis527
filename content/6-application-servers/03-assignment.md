---
title: "Assignment"
weight: 15
pre: "3. "
---

### Lab 6 - Application Servers

#### Instructions

Create **two** cloud systems and **four** virtual machines meeting the specifications given below. The best way to accomplish this is to treat this assignment like a checklist and check things off as you complete them.

If you have any questions about these items or are unsure what they mean, please contact the instructor. Remember that part of being a system administrator (and a software developer in general) is working within vague specifications to provide what your client is requesting, so eliciting additional information is a very necessary skill.

{{% notice note %}}
_To be more blunt - this specification may be purposefully designed to be vague, and it is your responsibility to ask questions about any vagaries you find. Once you begin the grading process, you cannot go back and change things, so be sure that your machines meet the expected specification regardless of what is written here. --Russ_
{{% /notice %}}

Also, to complete many of these items, you may need to refer to additional materials and references not included in this document. System administrators must learn how to make use of available resources, so this is a good first step toward that. Of course, there's always [Google](http://www.google.com)!

#### Time Expectation

This lab may take anywhere from **1 - 6 hours** to complete, depending on your previous experience working with these tools and the speed of the hardware you are using. Configuring application servers is very time-consuming the first time through the process, but it will be much more familiar by the end of this course.

{{% notice info %}}
_This lab involves working with resources on the cloud, and will require you to sign up and pay for those services. In general, your total cost should be low, usually around $20 total. If you haven't already, you can sign up for the [GitHub Student Developer Pack](https://education.github.com/pack) to get discounts on most of these items. If you have any concerns about using these services, please contact me to make alternative arrangements! --Russ_
{{% /notice %}}

---

### Task 0: Droplets & Virtual Machines

For this lab, you will continue to use the two DigitalOcean droplets from Lab 5, labelled **FRONTEND** and **BACKEND**, respectively. This assignment assumes you have completed all steps in Lab 5 successfully; if not, you should consult with the instructor to resolve any existing issues before continuing.

You will also need a Windows Server 2016 VM configured as an Active Directory Domain Controller, along with a Windows 10 VM added as a client computer on that domain. In general, you may continue to use the resources created in Lab 4, but you may choose to recreate them as directed in Lab 4 if desired.

In addition, you will need two Ubuntu VMs, one labelled **SERVER** and the other labelled **CLIENT**. You may continue to use the Ubuntu VMs from Labs 3 and 4, or create new VMs for this lab. This lab does not assume any existing setup on these VMs beyond what is specified in Labs 1 and 2. You should also make sure your Ubuntu VM labelled **SERVER** has a static IP address.  

---

### Task 1: Windows File Server

Configure a file server on your Windows Server 2016 VM. It should have the following features:

* A shared folder on the server named `everyone` and stored at `C:\everyone` that should be accessible by all users on your domain
* A shared folder on the server named `restricted` and stored at `C:\restricted` that should only be accessible to users in the Domain Admins group in your domain

#### Resources

* [How to Share Files and Folders in Windows Server 2016](https://www.tactig.com/share-files-folders-windows-server-2016/) from Tactig

---

### Task 2: Windows Group Policy

Configure group policy objects (GPOs) on your Windows Active Directory domain to perform the following tasks:

* All domain users should get the `everyone` folder automatically mapped to the `Z:\` drive on any system they log into.
* Users in the Domain Admins group should also get the `restricted` folder automatically mapped to the `Y:\` drive on any system they log into.  

{{% notice tip %}}
_Pay close attention to which OUs in the domain you attach these GPOs to. You can use the domain Administrator account and the other domain account created in Lab 4 to test these on your Windows 10 client. --Russ_
{{% /notice %}}

#### Resources

* **[Windows Group Policy]({{< relref "/4-directory-services/06-windows-group-policy" >}})**
* [How to Map Network Drives with Group Policy (Complete Guide)](https://activedirectorypro.com/map-network-drives-with-group-policy/) by Robert Allen on Active Directory Pro
* [How to: Mapping Network Drives/Folders via Group Policy](https://community.spiceworks.com/how_to/79280-mapping-network-drives-folders-via-group-policy) on Spiceworks Community

---

### Task 3: Ubuntu File Server

Configure a file server using Samba on your Ubuntu VM labelled **SERVER**. It should have the following features:

* A shared folder on the server named `everyone` and stored at `/everyone` that should be accessible by all Samba users
* Enable shared home directories in Samba using the default `[homes]` share.

#### Resources

* [File Server](https://help.ubuntu.com/lts/serverguide/samba-fileserver.html.en) from Ubuntu Documentation
* [Samba Server Guide](https://help.ubuntu.com/community/Samba/SambaServerGuide) from Ubuntu Community Help Wiki
* [How to Set Up a Samba Share for a Small Organization on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-samba-share-for-a-small-organization-on-ubuntu-16-04) from DigitalOcean (works for 18.04)
* [Access User's Home Folders via Samba on Ubuntu 17.04](https://websiteforstudents.com/access-user-home-folders-via-samba-on-ubuntu-17-04-17-10/) from Website for Students (works for 18.04)

---

### Task 4: Ubuntu Drive Mapping

Configure your Ubuntu VM labelled **CLIENT** to automatically access the Samba shares in the following manner:

* Add an entry to `\etc\fstab` to automatically mount the `everyone` folder to `/mnt/everyone` at system boot. It should be readable and writable by all users.
* Create a Bash script that will mount a user's home folder to `/mnt/home` when the user logs on. You will also need to make sure that script is properly triggered at login using `cron` or some other method. You should also configure a script to unmount the drive when the user logs off. The mounted share should be readable and writable by that user.

{{% notice tip %}}
_To create the script, first you must figure out how to perform the steps using the terminal. Then, you can simply place those commands in a script file and try to run the script itself. It is sufficient to perform these steps for the cis527 account only. Unfortunately, this approach does not scale well as it must be done on a per-user basis. If you know of a way to get this to work across all users, bug bounty points can be had! --Russ_
{{% /notice %}}

#### Resources

* **[Bash Scripting]({{< relref "/X-extras/03-bash-scripting" >}})**
* **[Cron (Linux Scheduled Tasks)]({{< relref "/X-extras/04-cron-linux-scheduled-tasks" >}})**
* [Mount Windows Shares Permanently](https://wiki.ubuntu.com/MountWindowsSharesPermanently) from Ubuntu Wiki
* [How Do I Access Windows Shares from Bash](https://askubuntu.com/questions/434358/how-do-i-access-windows-shares-from-bash) on Ask Ubuntu Forums

---

### Task 5: Windows Web Application Server

For this task, you will install and configure a .NET web application for IIS on your Windows Server 2016 VM. First, choose an application to install from the following list:

* [BlogEngine.NET](https://blogengine.io/)

If you would like to work with an application not listed here, please contact the instructor. The application should have some sort of functionality beyond just displaying static pages. Any approved application can be added to this list for you to use.

Once you have selected your application, perform the following configuration steps:

1. Follow the application's instructions to install and configure the application. Make sure you can access it at `http://localhost` before continuing
2. Configure the host header for that site to be `mywebsite.local`. To test this configuration, create a second website with static content that has a host header of `anothersite.local`
{{% notice tip %}}
_You'll need to add entries to your system's `hosts` file to redirect those domain names to the loopback IP address `127.0.0.1` --Russ_
{{% /notice %}}
3. Create a self-signed SSL certificate and attach it to that site
4. Configure URL redirection to automatically direct users from HTTP to HTTPS for that site

Once these steps are complete, visiting `http://mywebsite.local` in your web browser should automatically redirect you to `https://mywebsite.local` and it should be secured using your self-signed certificate. You should also be able to demonstrate that the application is working properly by interacting with it in some meaningful way. Finally, if you visit `http://anothersite.local` you should see the static content from that site.

{{% notice note %}}
_I recommend using Firefox for testing. Edge & Internet Explorer on Windows Server are locked-down by default and can be very frustrating to work with. --Russ_
{{% /notice %}}

#### Resources

* [Add A Website to Windows Server 2016 using Host Headers](https://helpdesk.ssls.com/hc/en-us/articles/115000853911-How-to-install-a-SSL-certificate-on-IIS-10) from 1&1
* [How to Create a Self Signed Certificate in IIS](https://aboutssl.org/how-to-create-a-self-signed-certificate-in-iis/) from AboutSSL
* [Microsoft Server 2016 - IIS 10 & 10.5 - SSL Installation](https://www.sslsupportdesk.com/microsoft-server-2016-iis-10-10-5-ssl-installation/) from SSLSupportDesk
* [How to Install a SSL Certificate on IIS 10](https://helpdesk.ssls.com/hc/en-us/articles/115000853911-How-to-install-a-SSL-certificate-on-IIS-10) from SSLs.com
* [Redirect from HTTP to HTTPS using the IIS URL Rewrite Module](https://blogs.technet.microsoft.com/dawiese/2016/06/07/redirect-from-http-to-https-using-the-iis-url-rewrite-module/) from Microsoft TechNet

---

### Task 6: Ubuntu Web Application Server

For this step, you will install and configure a web application running on Apache in Ubuntu on your DigitalOcean droplets. First, choose an application to install from the following list:

* [Wordpress](https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-with-lamp-on-ubuntu-18-04)
* [Booked](https://www.bookedscheduler.com/)

If you would like to work with an application not listed here, please contact the instructor. The application should have some sort of functionality beyond just displaying static pages, and must support using a MySQL database on a separate host from the web server. In addition, the application must be installed manually - using pre-built images or Apt packages is not allowed here. Any approved application can be added to this list for you to use.

Once you have selected your application, perform the following configuration steps:

1. Install MySQL (and optionally phpMyAdmin) on your Ubuntu droplet labelled **BACKEND** and configure an appropriate username and database for your application
{{% notice tip %}}
_You may need to configure MySQL to listen on an external network interface. Make sure you use the private network IP address. In addition, you may also have to open ports on the firewall. --Russ_
{{% /notice %}}
2. Configure a new virtual host in Apache for your web application. Also, add an appropriate A record to your domain name created in Lab 5 for this virtual host
3. Install your web application on your Ubuntu droplet labelled **FRONTEND** following the application's installation instructions. When configuring the database for your application, you should have it use the MySQL database on **BACKEND** via the private network IP address
4. Use CertBot to obtain an SSL certificate for your new application, and have it automatically configure redirection from HTTP to HTTPS

Once these steps are complete, you should be able to visit your web application via HTTP, see it automatically redirect you to HTTPS, confirm that the SSL certificate is installed and valid, and then interact with the application in some meaningful way to confirm that the database connection is working. Of course, the two virtual hosts configured in Lab 5 should continue to work as well.

#### Resources

* [Install MySQL on Ubuntu 18.04 Bionic Beaver Linux](https://linuxconfig.org/install-mysql-on-ubuntu-18-04-bionic-beaver-linux) from LinuxConfig.org
* [How To Install and Secure phpMyAdmin on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-18-04) from DigitalOcean
* [How To Install the Apache Web Server on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-18-04) from DigitalOcean
* [How To Secure Apache with Let's Encrypt on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-18-04) from DigitalOcean

---

### Task 7: Make Snapshots

In each of the virtual machines created above, create a snapshot labelled "Lab 6 Submit" before you submit the assignment. The grading process may require making changes to the VMs, so this gives you a restore point before grading starts.

### Task 8: Schedule A Grading Time

Contact the instructor and schedule a time for interactive grading. You may continue with the next module once grading has been completed.
