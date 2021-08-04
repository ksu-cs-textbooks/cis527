---
title: "Assignment"
weight: 20
pre: "4. "
---

### Lab 7 - Backups, Monitoring & DevOps

#### Instructions

Create **two** cloud systems and **four** virtual machines meeting the specifications given below. The best way to accomplish this is to treat this assignment like a checklist and check things off as you complete them.

If you have any questions about these items or are unsure what they mean, please contact the instructor. Remember that part of being a system administrator (and a software developer in general) is working within vague specifications to provide what your client is requesting, so eliciting additional information is a very necessary skill.

{{% notice note %}}
_To be more blunt - this specification may be purposefully designed to be vague, and it is your responsibility to ask questions about any vagaries you find. Once you begin the grading process, you cannot go back and change things, so be sure that your machines meet the expected specification regardless of what is written here. --Russ_
{{% /notice %}}

Also, to complete many of these items, you may need to refer to additional materials and references not included in this document. System administrators must learn how to make use of available resources, so this is a good first step toward that. Of course, there's always [Google](http://www.google.com)!

#### Time Expectation

This lab may take anywhere from **1 - 6 hours** to complete, depending on your previous experience working with these tools and the speed of the hardware you are using. Working with each of these items can be very time-consuming the first time through the process, but it will be much more familiar by the end of this course.

{{% notice info %}}
_This lab involves working with resources on the cloud, and will require you to sign up and pay for those services. In general, your total cost should be low, usually around $20 total. If you haven't already, you can sign up for the [GitHub Student Developer Pack](https://education.github.com/pack) to get discounts on most of these items. If you have any concerns about using these services, please contact me to make alternative arrangements! --Russ_
{{% /notice %}}

---

### Task 0: Droplets & Virtual Machines

For this lab, you will continue to use the two DigitalOcean droplets from Labs 5 and 6, labelled **FRONTEND** and **BACKEND**, respectively. This assignment assumes you have completed all steps in the previous labs successfully; if not, you should consult with the instructor to resolve any existing issues before continuing.

You will also need a Windows Server 2019 VM configured as an Active Directory Domain Controller, along with a Windows 10 VM added as a client computer on that domain. You should continue to use the systems from Lab 6.

Finally, you will need two Ubuntu 20.04 VMs, but they don't need any particular configuration beyond what is specified in Lab 1 or Lab 2. You may continue to use your Ubuntu VMs from Lab 6. 

---

### Task 1: Backup & Restore Windows Active Directory

This task requires you to successfully demonstrate a backup and restore procedure for your Windows Server 2016 Active Directory domain. To complete this item, follow these steps:

1. Create a user named `backupuser` on your Active Directory domain
2. Create a group named `BackupGroup` on your Active Directory domain, and add the new `backupuser` user to that group
3. Log on to your Windows 10 client VM as `backupuser` and take a **screenshot** showing the successful login and the system time of your host system.
4. Create a backup of your Active Directory domain using the Windows System State backup tool. You should store this backup on an external hard disk, such as a flash drive, that is mounted in your Windows Server 2019 VM. Alternatively, you may add a secondary hard disk to your Windows Server 2019 VM and use that location to store the backup. See the video in the resources section for instructions.
5. Once the backup is complete, delete the `backupuser` user and `BackupGroup` group from the Active Directory domain.
6. Reboot your Windows 10 client VM and attempt to log on as `backupuser`. It should fail. Take a **screenshot** showing a failed login and the system time of your host system
7. Perform an authoritative restore of the Active Directory domain from the backup. This should restore the deleted user and group. Take a **screenshot** showing the successful completion of the authoritative restore process and the system time of your host system. 

{{% notice info %}}
_The documentation for this portion is unclear. In my testing, you may be able to just checkmark the "Perform an authoritative restore of Active Directory files" option when restoring the backup and avoid any command-line work. That seems to be working correctly as of Summer 2021. However, if that doesn't work or you choose to do the authoritative restore via command-line, you need to get the path correct. To help with that, here's a hint: for my sample domain `ad.russfeld.cis527.cs.ksu.edu` and account `backupuser`, I'll need to use the command `restore object "cn=backupuser,cn=Users,dc=ad,dc=russfeld,dc=cis527,dc=cs,dc=ksu,dc=edu"` to restore the correct account on the domain. --Russ_
{{% /notice %}}

8. Reboot your Windows 10 client VM and log on to that system as `backupuser`. Take a **screenshot** showing the successful login and the system time of your host system.

{{% notice tip %}}
_You'll present those 4 screenshots as part of the grading process for this lab, so I recommend storing them somewhere memorable so they are easy to find. --Russ_
{{% /notice %}}

#### Resources

These resources mostly refer to Windows Server 2012 or 2016, but should work for 2019 as well. 

* [AD Forest Recovery - Backing up a full server](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/manage/ad-forest-recovery-backing-up-a-full-server) from Microsoft Windows IT Pro Center
* [How to Backup Active Directory Fully in Windows Server 2016](https://www.tactig.com/backup-active-directory-windows-server/) from Tactig
* [How to perform Authoritative Restore of Active Directory Objects - 2012 R2](http://www.itingredients.com/perform-authoritative-restore-active-directory-objects-2012-r2/) from ITIngredients (should work for 2019)
* [Windows Server 2012 - Active Directory - Backup and Restore, Part 1: System State](http://davidmtechblog.blogspot.com/2014/01/windows-server-2012-active-directory_10.html) from David M Tech Blog (should work for 2019)
* [How to Add Additional Virtual Hard Disk Drive in VMWare Workstation Tutorial](https://www.youtube.com/watch?v=WMPd0kF4JLM) by The Teacher on YouTube

---

### Task 2: Backup Ubuntu Web Application

For this task, you will perform the steps to create a backup of the web application installed on your Ubuntu droplet in Lab 6. To complete this item, prepare an archive file (`.zip`, `.tar`, `.tgz` or equivalent) containing the following items:

1. Website data and configuration files for the web application (this should NOT include the entire application, just the relevant configuration and data files that were modified after installation)
2. Relevant Apache configuration files (virtual hosts)
3. A complete MySQL server dump of the appropriate MySQL database. It should contain enough information to recreate the database schema and all data.
4. Clear, concise instructions in a README file for restoring this backup on a new environment. Assume the systems in that new environment are configured as directed in Lab 5. These instructions would be used by yourself or a system administrator of similar skill and experience to restore this application - that is, you don't have to pedantically spell out how to perform every step, but you should provide enough information to easily reinstall the application and restore the backup with a minimum of effort and research.

#### Resources

* [How to Compress and Extract Files using the tar Command on Linux](https://www.howtogeek.com/248780/how-to-compress-and-extract-files-using-the-tar-command-on-linux/) from How-To Geek
* [How to Import and Export Databases and Reset a Root Password in MySQL](https://www.digitalocean.com/community/tutorials/how-to-import-and-export-databases-and-reset-a-root-password-in-mysql) from DigitalOcean
* [How To Backup MySQL Databases on an Ubuntu VPS](https://www.digitalocean.com/community/tutorials/how-to-backup-mysql-databases-on-an-ubuntu-vps) from DigitalOcean (steps should still be valid for 20.04)

---

### Task 3: Ubuntu Monitoring Part 1

For this task, you will set up either Munin or Ganglia on your Ubuntu droplets from Lab 6. To complete this item, follow these steps:

1. Configure the Ubuntu droplet named **FRONTEND** as the primary server for either Munin or Ganglia.
2. Add the Ubuntu droplet named **BACKEND** as a client on either Munin or Ganglia
3. Send the URL of the Munin or Ganglia server in your grading packet. Make sure that both **FRONTEND** and **BACKEND** are appearing in the data. 


Of course, you may need to modify your firewall configuration to allow incoming connections for Munin! **If your firewall is disabled and/or not configured, there will be a deduction of up to 10% of the total points on this lab**

{{% notice tip %}}
_As always, you may have to deal with Apache virtual hosts and firewalls for this setup. In addition, you may want to add a new A record to your domain name for this site, and request an SSL certificate via CertBot. --Russ_
{{% /notice %}}

#### Resources

* [Server Monitoring with Munin and Monit on Ubuntu 16.04 LTS (Xenial Xerus)](https://www.howtoforge.com/tutorial/server-monitoring-with-munin-and-monit-on-ubuntu-16-04-lts/) from HowtoForge (should work on 20.04)
* [How to Install the Munin Monitoring Tool on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-install-the-munin-monitoring-tool-on-ubuntu-14-04) from DigitalOcean (should work on 20.04)
* [How to Install and Configure Ganglia Monitor on Ubuntu 16.04](https://hostpresto.com/community/tutorials/how-to-install-and-configure-ganglia-monitor-on-ubuntu-16-04/) from HostPresto (should work on 20.04)
* [Introduction to Ganglia on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/introduction-to-ganglia-on-ubuntu-14-04) from DigitalOcean (should work on 20.04)

---

### Task 4: DevOps

Setup an automatically deployed Git repository on your Ubuntu droplet. For this task, perform the following:

1. Create a GitLab repository on the [K-State CS GitLab](https://gitlab.cs.ksu.edu/) instance.
2. Clone that repository on your own system, and verify that you can make changes, commit them, and push them back to the server.
3. Clone that repository into a web directory on your Ubuntu droplet named **FRONTEND**. You can use the default directory first created in Lab 5.
4. Create a Bash script that will simply use the `git pull` command to get the latest content from the Git repository in the current directory.
5. Install and configure [webhook](https://github.com/adnanh/webhook) on your Ubuntu droplet named **FRONTEND**. It should listen for all incoming webhooks from GitLab that match a secret key you choose. When a hook is received, it should run the Bash script created earlier.
6. Configure a webhook in your GitLab repository for all Push events using that same secret key and the URL of webhook on your server. You may need to make sure your domain name has an A record for the default hostname `@` pointing to your **FRONTEND** server.
7. To test this setup, you should be able to push a change to the GitLab repository, and see that change reflected on the website automatically.
8. For offline grading, add the instructor and GTA to the repository as maintainers, and submit the repository and URL where the files can be found in your grading packet. Provided the webhook works correctly, they should be able to see a pushed change to the repository update the website. 

Of course, you may need to modify your firewall configuration to allow incoming connections for Webhook! **If your firewall is disabled and/or not configured, there will be a deduction of up to 10% of the total points on this lab**

{{% notice tip %}}
_Since the Webhook process runs as the `root` user on **FRONTEND**, you'll need to make sure a set of SSH keys exist in the `root` user's home folder `/root/.ssh/` and add the public key from that directory to your [GitLab account](https://gitlab.cs.ksu.edu/profile/keys). You should then use the root account (use `sudo su -` to log in as root) to run `git pull` from the appropriate directory on **FRONTEND** at least once so you can accept the SSH fingerprint for the GitLab server. This helps ensure that `root` can properly run the script. --Russ_
{{% /notice %}}

#### Resources

* **[Extras - Git]({{< relref "/X-extras/07-git" >}})**
* [webhook](https://github.com/adnanh/webhook) on GitHub
* [webhook Hook Examples](https://github.com/adnanh/webhook/blob/master/docs/Hook-Examples.md) on GitHub
* [Webhooks](https://docs.gitlab.com/ee/user/project/integrations/webhooks.html) on GitLab Documentation

---

### EXTRA CREDIT TASK: Ubuntu Monitoring Part 2

{{% notice note %}}

This task is worth 10 points extra credit toward your overall lab grade. It can be tricky to perform, since you need to provide significant amounts of RAM to your Ubuntu system for it to work. Don't worry too much if you can't get it to work - I struggle with this one sometimes! -Russ

{{% /notice %}}

For this task, you will install Elasticsearch, Logstash, and Kibana (a.k.a. the Elastic Stack, sometimes known as the ELK stack) on your Ubuntu 20.04 VMs, and configure both Filebeat and Metricbeat to collect information about those hosts. 

1. On the Ubuntu VM you'll be using as the server, make sure you have **at least 4GB of RAM** assigned to the VM. Unfortunately, Elasticsearch and Kibana won't run properly with less than 4GB of RAM available. 
2. Follow the instructions in the DigitalOcean guide to install the Elastic stack on one of your Ubuntu VMs. 
    * If you already have Apache installed on this system, I recommend changing the port for nginx to something other than 80, such as 8080. This can be done in the nginx configuration file for the site that is created in the guide.
3. Install Filebeat on that VM, and configure it to send data through Logstash following the instructions on the DigitalOcean guide. 
4. Confirm that you can access data from Filebeat/Logstash in Kibana before continuing. 
5. Using the other DigitalOcean guide, install Metricbeat on both Ubuntu VMs. 
    * Metricbeat should be configured to directly send data to Elasticsearch, without going through Logstash 
    * Don't forget to allow the appropriate ports through the firewall
    * You'll need to configure Elastic Search for [Single-node discovery](https://www.elastic.co/guide/en/elasticsearch/reference/master/bootstrap-checks.html#single-node-discovery) or else it won't start
6. Verify that you can see metric data such as CPU usage in Kibana (look for the **[Metricbeat System] Overview ECS** dashboard). 
7. Take a screenshot of the **[Metricbeat System] Overview ECS** and add it to your grading packet. Alternatively, schedule a time for grading to review this part of the lab.

#### Resources

* [How to Install Elasticsearch, Logstash, and Kibana (Elastic Stack) on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-elastic-stack-on-ubuntu-20-04) from DigitalOcean
* [How to Gather Infrastructure Metrics with Metricbeat on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-gather-infrastructure-metrics-with-metricbeat-on-ubuntu-18-04) from DigitalOcean (should work on 20.04 as well)
* [Install ELK on Ubuntu 20.04 Focal Fossa Linux](https://linuxconfig.org/install-elk-on-ubuntu-20-04-focal-fossa-linux) from Linuxconfig.org
* [Elasticsearch Boostrap Checks](https://www.elastic.co/guide/en/elasticsearch/reference/master/bootstrap-checks.html#single-node-discovery) from Elastic.co (for configuring single-node discovery)

---

### Task 6: Submit Files

This lab may be graded completely offline. To do this, submit the following items via Canvas:

1. **Task 1**: 4 screenshots clearly showing the system time, showing a successful login before the test user is deleted, an unsuccessful login after the user was deleted, a successful restoration of the AD, and a successful login showing that the user was restored.
2. **Task 2**: An archive file containing a README document as well as any files or information needed as part of the backup of the Ubuntu web application installed in Lab 6.
3. **Task 3**: The URL of your Munin or Ganglia instance, clearly showing data from both **FRONTEND** and **BACKEND**. 
4. **Task 4**: A GitLab repository URL and a URL of the website containing those files. Make sure the instructor and GTA are added to the repository as maintainers. They should be able to push to the repository and automatically see the website get updated. 
5. **Extra Credit Task**: A screenshot of the **[Metricbeat System] Overview ECS** dashboard showing data from both Ubuntu VMs

If you are able to submit all 5 of the items above, you do not need to schedule a grading time. The instructor or GTA will contact you for clarification if there are any questions on your submission.

For Tasks 3 - 5, you may also choose to do interactive grading, especially if you were unable to complete it and would like to receive partial credit. 

### Task 7: Schedule A Grading Time

If you are not able to submit information for all 5 tasks for offline grading, you may contact the instructor and schedule a time for interactive grading. You may continue with the next module once grading has been completed.
