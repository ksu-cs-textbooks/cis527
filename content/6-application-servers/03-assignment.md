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

You will also need a Windows Server 2022 VM configured as an Active Directory Domain Controller, along with a Windows 11 VM added as a client computer on that domain. In general, you may continue to use the resources created in Lab 4, but you may choose to recreate them as directed in Lab 4 if desired.

In addition, you will need two Ubuntu VMs, one labelled **SERVER** and the other labelled **CLIENT**. You may continue to use the Ubuntu VMs from Labs 3 and 4, or create new VMs for this lab. This lab does not assume any existing setup on these VMs beyond what is specified in Labs 1 and 2. You should also make sure your Ubuntu VM labelled **SERVER** has a static IP address.  

---

### Task 1: Windows File Server

Configure a file server on your Windows Server 2022 VM. It should have the following features:

* A shared folder on the server named `public` and stored at `C:\public` that should be accessible by all users on your domain
* A shared folder on the server named `admins` and stored at `C:\admins` that should only be accessible to users in the Domain Admins group in your domain

{{% notice tip %}}

As of Summer 2021, there was a bug in Windows Server that prevented the built-in Administrator account from changing some settings, specifically network settings, once the server is promoted to a domain controller. This can make it difficult to fix networking issues in this or future labs. The easy fix for this is to copy the Administrator account in the Active Directory User and Computers tool and give the new copy a different name, such as "Admin", and then use that account to log on to the server. 

{{% /notice %}}

#### Resources

* [How to Share Files and Folders in Windows Server 2016](https://www.tactig.com/share-files-folders-windows-server-2016/) from Tactig (should work for Server 2022)

---

### Task 2: Windows Group Policy

Configure group policy objects (GPOs) on your Windows Active Directory domain to perform the following tasks:

* All domain users should get the `public` folder automatically mapped to the `Z:\` drive on any system they log into.
* Users in the ``Domain Admins`` group should also get the `admins` folder automatically mapped to the `Y:\` drive on any system they log into. 
   * That drive **should not** be mapped for any user that is not a member of the `Domain Admins` group. 

{{% notice tip %}}
_Pay close attention to how you attach and target these GPOs in the domain. You can use the domain Administrator account and the other domain account created in Lab 4 to test these on your Windows 11 client. --Russ_
{{% /notice %}}

#### Resources

* **[Windows Group Policy]({{% relref "/4-directory-services/06-windows-group-policy"  %}})**
* [How to Map Network Drives with Group Policy (Complete Guide)](https://activedirectorypro.com/map-network-drives-with-group-policy/) by Robert Allen on Active Directory Pro
* [How to: Mapping Network Drives/Folders via Group Policy](https://community.spiceworks.com/how_to/79280-mapping-network-drives-folders-via-group-policy) on Spiceworks Community

---

### Task 3: Ubuntu File Server

Configure a file server using Samba on your Ubuntu VM labelled **SERVER**. It should have the following features:

* A shared folder on the server named `public` and stored at `/public` that should be accessible by all Samba users
* Enable shared home directories in Samba using the default `[homes]` share.
* Enable the `cis527` user in the Samba password database. It should use the same `cis527_linux` password as the actual `cis527` account.

Of course, you may need to modify your firewall configuration to allow incoming connections to the file server! **If your firewall is disabled and/or not configured, there will be a deduction of up to 10% of the total points on this lab**

#### Resources

* [File Server](https://ubuntu.com/server/docs/samba-file-server) from Ubuntu Documentation
* [How to Set Up a Samba Share for a Small Organization on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-samba-share-for-a-small-organization-on-ubuntu-16-04) from DigitalOcean (works for 24.04)
* [Access User's Home Folders via Samba on Ubuntu 17.04](https://websiteforstudents.com/access-user-home-folders-via-samba-on-ubuntu-17-04-17-10/) from Website for Students (works for 24.04)
* [How to Configure Samba Server Share on Ubuntu 20.04 Focal Fossa Linux](https://linuxconfig.org/how-to-configure-samba-server-share-on-ubuntu-20-04-focal-fossa-linux) from LinuxConfig.org

---

### Task 4: Ubuntu Drive Mapping

Configure your Ubuntu VM labelled **CLIENT** to automatically access the Samba shares in the following manner:

* Add an entry to `\etc\fstab` to automatically mount the `public` folder to `/mnt/public` at system boot. It should be readable and writable by all users.
* Use `libpam-mount` to automatically mount a user's `homes` share from the server at login. This only needs to work for the `cis527` user, as that user should be present on both systems and Samba.

{{% notice note %}}
_To be honest, this last part can be pretty tricky. I recommend following the instructions in this video in this module very carefully. If you have any issues, you can enable debugging and review `/var/log/syslog` for errors. --Russ_
{{% /notice %}}

#### Resources

* [Mount Windows Shares Permanently](https://wiki.ubuntu.com/MountWindowsSharesPermanently) from Ubuntu Wiki
* [How Do I Access Windows Shares from Bash](https://askubuntu.com/questions/434358/how-do-i-access-windows-shares-from-bash) on Ask Ubuntu Forums
* [Use of pam-mount to Mount Home from Server](https://ubuntuforums.org/showthread.php?t=1375653) on Ubuntu Forums
* [pam_mount](http://manpages.ubuntu.com/manpages/bionic/man8/pam_mount.8.html) on Ubuntu Manpages
* [pam_mount.conf](http://manpages.ubuntu.com/manpages/bionic/man5/pam_mount.conf.5.html) on Ubuntu Manpages

---

### Task 5: Windows Web Application Server

For this task, you will install and configure a .NET web application for IIS on your Windows Server 2022 VM. First, choose an application to install from the following list:

* [BlogEngine.NET](https://blogengine.io/docs/get-started/)
  * **NOTE**: If you choose BlogEngine.NET, make sure you read their site carefully. You don't have to sign up for anything on their site to download the software itself, but the download link tends to be hidden in favor of their hosted options. As a sysadmin, you should definitely get into the habit of carefully reading and considering what you find online before you click!

If you would like to work with an application not listed here, please contact the instructor. The application should have some sort of functionality beyond just displaying static pages. Any approved application can be added to this list for you to use. **_You are not allowed to use JitBit's .NET Forum, as that was demonstrated in the video in this module._**

Once you have selected your application, perform the following configuration steps:

1. Create two websites in IIS: `blog.<your eID>.cis527.org` and `site.<your eID>.cis527.org`. They should be stored in `C:\inetpub\blog` and `C:\intepub\site`, respectively. For the `blog` site, make sure you choose the `.NET v4.5` Application Pool!
2. Add a DNS forward lookup zone for `<your eID>.cis527.org` to the Windows DNS server, and then add A records for the two sites described above. They should both point to the Windows Server's IP address ending in `.42`.
3. Place a static HTML file inside of the `C:\intepub\site` folder and confirm that you can access it using Firefox at `http://site.<your eID>.cis527.org`
4. Follow the instructions to install and configure your chosen application in `C:\inetpub\blog`. Pay special attention to any file permissions required. Use the `IIS_IUSRS` group when adding write permissions to any folders as described in the instructions. You should be able to access it at `http://blog.<your eID>.cis527.org` using Firefox. 
5. Create a self-signed SSL certificate and attach it to both websites by adding an additional binding for HTTPS. Make sure you can access both websites using `https://`. 
6. Use the URL Rewrite module to configure URL redirection to automatically direct users from HTTP to HTTPS for both websites.

Once these steps are complete, visiting `http://blog.<your eID>.cis527.org` in your web browser should automatically redirect you to `https://blog.<your eID>.cis527.org` and it should be secured using your self-signed certificate. You should also be able to demonstrate that the application is working properly by interacting with it in some meaningful way, such as logging in and making a new post on a blog. Finally, if you visit `http://site.<your eID>.cis527.org` you should see the static content from that site instead of the blog, and it should also properly redirect to HTTPS.

{{% notice note %}}
_I recommend using Firefox for testing. Edge & Internet Explorer on Windows Server are locked-down by default and can be very frustrating to work with. See, I knew you'd appreciate having Firefox installed on your Windows server! --Russ_
{{% /notice %}}

#### Resources

* **[URL Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) from Microsoft**
* [Add A Website to Windows Server 2016 using Host Headers](https://www.ionos.com/digitalguide/hosting/technical-matters/add-a-website-to-windows-server-2016-using-host-headers/) from Ionos by 1&1
* [How to add DNS Forward Lookup Zone in Windows Server 2019](https://computingforgeeks.com/how-to-add-dns-forward-lookup-zone-in-windows-server/) from Computingforgeeks
* [How to add DNS A/PTR Record in Windows Server 2019](https://computingforgeeks.com/how-to-add-dns-a-ptr-record-in-windows-server/) from Computingforgeeks
* [How to Create a Self Signed Certificate in IIS](https://aboutssl.org/how-to-create-a-self-signed-certificate-in-iis/) from AboutSSL
* [Microsoft Server 2016 - IIS 10 & 10.5 - SSL Installation](https://www.sslsupportdesk.com/microsoft-server-2016-iis-10-10-5-ssl-installation/) from SSLSupportDesk
* [How to Install a SSL Certificate on IIS 10](https://www.thesslstore.com/knowledgebase/ssl-install/microsoft-iis-10-ssl-installation/) from SSLs.com
* [Setting up an HTTP/HTTPS Redirect in IIS](https://www.namecheap.com/support/knowledgebase/article.aspx/9953/38/setting-up-an-httphttps-redirect-in-iis) from Namecheap

---

### Task 6: Ubuntu Web Application Server

For this step, you will install and configure a web application running in Ubuntu on your DigitalOcean droplets. First, choose an application to install from the following list:

* [Wordpress](https://wordpress.org/download/)

If you would like to work with an application not listed here, please contact the instructor. The application should have some sort of functionality beyond just displaying static pages, and must support using a MySQL database on a separate host from the web server. In addition, the application must be installed manually - using pre-built images or Apt packages is not allowed here. Any approved application can be added to this list for you to use. **_You are not allowed to use phpBB, as that was demonstrated in the video in this module._**

{{% notice warning %}}

MySQL Version 8 and later requires at least 1 GB of RAM to run properly. I recommend resizing the droplet you will use for MySQL to have at least 1 GB of RAM for this step. [How to Resize Droplets](https://docs.digitalocean.com/products/droplets/how-to/resize/).

Alternatively you can use MySQL 5.7 via Docker in Option 2, or add [swap space on Ubuntu (not recommended)](https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-22-04).

{{% /notice %}}

Once you have selected your application, choose **ONE** of the following configuration options:

##### Option 1: Bare Hardware

1. Install MySQL (and optionally phpMyAdmin) on your Ubuntu droplet labelled **BACKEND** and configure an appropriate username and database for your application. You should also enable SSL/TLS encryption on connections to the server if it is not already enabled in MySQL (this should be enabled by default in Ubuntu 20.04). When creating the user account in MySQL, make sure it is set to log in from the private network IP address of **FRONTEND**.
{{% notice tip %}}
_You may need to configure MySQL to listen on an external network interface. Make sure you use the private network IP address only - it should not be listening on all network interfaces. In addition, you will also have to open ports on the firewall, and you should restrict access to those ports to only allow connections from the private network IP address of **FRONTEND**, just like the SSH server in Lab 5. Points will be deducted for having a MySQL server open to the internet! --Russ_
{{% /notice %}}
2. Install Apache and configure a new virtual host in Apache for your web application on **FRONTEND**. Also, add an appropriate A record to your domain name created in Lab 5 for this virtual host. You may shut down any Docker containers from Lab 5 that interfere with this configuration. 
3. Install your web application on your Ubuntu droplet labelled **FRONTEND** following the application's installation instructions. When configuring the database for your application, you should have it use the MySQL database on **BACKEND** via the private network IP address. 
4. Of course, you may need to modify your firewall configuration to allow incoming connections to the database server! **If your firewall is disabled and/or not configured, there will be a deduction of up to 10% of the total points on this lab**

##### Option 2: Docker

1. Create two Docker containers on **FRONTEND**, one containing MySQL and another containing Wordpress. You may optionally add a container running phpMyAdmin if desired. The MySQL container must be isolated on its own internal network that cannot access the outside internet. 
2. Add an appropriate A record to your domain name created in Lab 5 for this docker container. You will also need to update your reverse proxy to properly route traffic to the Wordpress container. 
3. Make sure that Wordpress is properly configured via environment variables in Docker.

Once these steps are complete, you should be able to visit your web application via HTTP and then interact with the application in some meaningful way to confirm that the database connection is working.

#### Resources

* [Docker Wordpress Image](https://hub.docker.com/_/wordpress)
* [Install MySQL on Ubuntu 20.04 LTS Linux](https://linuxconfig.org/install-mysql-on-ubuntu-20-04-lts-linux) from LinuxConfig.org
* [How To Install MySQL on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-22-04) from DigitalOcean (follow instructions in guide above to configure  MySQL to listen on all network interfaces)
* [How To Install and Secure phpMyAdmin on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-22-04) from DigitalOcean
* [How To Install the Apache Web Server on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-22-04) from DigitalOcean
* [How To Secure Apache with Let's Encrypt on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-22-04) from DigitalOcean
* [How To Set Up A Remote Database to Optimize Site Performance with MySQL on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-remote-database-to-optimize-site-performance-with-mysql-on-ubuntu-20-04) from DigitalOcean (works for 22.04)

---

### Task 7: Make Snapshots

In each of the virtual machines created above, create a snapshot labelled "Lab 6 Submit" before you submit the assignment. The grading process may require making changes to the VMs, so this gives you a restore point before grading starts.

### Task 8: Schedule A Grading Time

Contact the instructor and schedule a time for interactive grading. You may continue with the next module once grading has been completed.
