---
title: "Assignment"
weight: 20
pre: "4. "
---

### Lab 7 - Backups, Monitoring & DevOps

#### Instructions

Create **two** cloud systems meeting the specifications given below. The best way to accomplish this is to treat this assignment like a checklist and check things off as you complete them.

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

---

### Task 1: Backup Ubuntu Web Application

For this task, you will perform the steps to create a backup of the web application installed on your Ubuntu droplet in Lab 6. To complete this item, prepare an archive file (`.zip`, `.tar`, `.tgz` or equivalent) containing the following items:

1. Website data and configuration files for the web application. This should NOT include the entire application, just the relevant configuration and data files that were modified after installation. For Docker installations, any information required to recreate the Docker environment, such as a Docker Compose file, should also be included.
2. Relevant Apache or Nginx configuration files (virtual hosts, reverse proxy, etc.)
3. A complete MySQL server dump of the appropriate MySQL database. It should contain enough information to recreate the database schema and all data.
4. Clear, concise instructions in a README file for restoring this backup on a new environment. Assume the systems in that new environment are configured as directed in Lab 5. These instructions would be used by yourself or a system administrator of similar skill and experience to restore this application - that is, you don't have to pedantically spell out how to perform every step, but you should provide enough information to easily reinstall the application and restore the backup with a minimum of effort and research.

#### Resources

* [How to Compress and Extract Files using the tar Command on Linux](https://www.howtogeek.com/248780/how-to-compress-and-extract-files-using-the-tar-command-on-linux/) from How-To Geek
* [How to Import and Export Databases and Reset a Root Password in MySQL](https://www.digitalocean.com/community/tutorials/how-to-import-and-export-databases-and-reset-a-root-password-in-mysql) from DigitalOcean
* [How To Backup MySQL Databases on an Ubuntu VPS](https://www.digitalocean.com/community/tutorials/how-to-backup-mysql-databases-on-an-ubuntu-vps) from DigitalOcean (steps should still be valid for 24.04)

---

### Task 2: Ubuntu Monitoring

For this task, you will set up Munin to monitor your servers.

1. Configure the Ubuntu droplet named **FRONTEND** as the primary host for Munin.
2. Then, add the **FRONTEND** and **BACKEND** droplets as two monitored hosts
3. Send the URL of the Munin dashboard and the password in your grading packet. Make sure that both **FRONTEND** and **BACKEND** are appearing in the data. 

Of course, you may need to modify your firewall configuration to allow incoming connections on the correct port for this to work! 

{{% notice tip %}}
_By default, Munin only allows access to the Munin dashboard from localhost. You'll need to modify the file `/etc/munin/apache24.conf` to allow access to external clients by removing any references to `Require Local` and adding different permissions instead. This [StackOverflow Answer](https://stackoverflow.com/a/12058057) gives the details._

_Once Munin is working, it may take a while for data to populate in the graphs. I generally check the "Memory usage - by day" graph as it seems to update the most frequently._
{{% /notice %}}

#### Resources

* [How to install and configure Munin](https://documentation.ubuntu.com/server/how-to/observability/install-munin/)
* [Fix Munin Permissions (StackOverflow)](https://stackoverflow.com/a/12058057)

---

### Task 3: DevOps

Setup an automatically deployed Git repository on your Ubuntu droplet. For this task, perform the following.

#### Option 1 - CS GitLab

1. Create a GitLab repository on the [K-State CS GitLab](https://gitlab.cs.ksu.edu/) instance. That repository must be public and clonable via HTTPS without any authenication. Unfortunately K-State blocks cloning repositories via SSH.
2. Clone that repository on your own system, and verify that you can make changes, commit them, and push them back to the server.
3. Clone that repository into a web directory on your Ubuntu droplet named **BACKEND**. You can use the default directory first created in Lab 5 (it should be `cis527charlie` in your DNS).
4. Create a Bash script that will simply use the `git pull` command to get the latest content from the Git repository in the current directory.
5. Install and configure [webhook](https://github.com/adnanh/webhook) on your Ubuntu droplet named **BACKEND**. It should listen for all incoming webhooks from GitLab that match a secret key you choose. When a hook is received, it should run the Bash script created earlier.
6. Configure a webhook in your GitLab repository for all Push events using that same secret key and the URL of webhook on your server. You may need to make sure your domain name has an A record for the default hostname `@` pointing to your **BACKEND** server.
7. To test this setup, you should be able to push a change to the GitLab repository, and see that change reflected on the website automatically.
8. For offline grading, add the instructor (@russfeld) to the repository as maintainers, and submit the repository and URL where the files can be found in your grading packet. Provided the webhook works correctly, they should be able to see a pushed change to the repository update the website. 

Of course, you may need to modify your firewall configuration to allow incoming connections for Webhook! **If your firewall is disabled and/or not configured, there will be a deduction of up to 10% of the total points on this lab**

{{% notice tip %}}
_In the video I use SSH to connect to GitLab, but that is no longer allowed through K-State's firewall. You'll need to create a public repository and clone it using HTTPS without authentication for this to work. Alternatively, you can use Option 2 below to configure this through GitHub instead.--Russ_
{{% /notice %}}

#### Option 2 - GitHub

1. Create a GitHub repository on the [GitHub](https://github.com/) instance. That repository may be public or private. If private, the repository should be set up to be cloned via SSH.
2. Clone that repository on your own system, and verify that you can make changes, commit them, and push them back to the server.
3. Clone that repository into a web directory on your Ubuntu droplet named **BACKEND**. You can use the default directory first created in Lab 5 (it should be `cis527charlie` in your DNS).
4. Create a Bash script that will simply use the `git pull` command to get the latest content from the Git repository in the current directory.
5. Install and configure [webhook](https://github.com/adnanh/webhook) on your Ubuntu droplet named **BACKEND**. It should listen for all incoming webhooks from GitHub that match a secret key you choose. When a hook is received, it should run the Bash script created earlier.
6. Configure a webhook in your GitHub repository for all Push events using that same secret key and the URL of webhook on your server. You may need to make sure your domain name has an A record for the default hostname `@` pointing to your **BACKEND** server.
  1. Alternatively, you may configure a GitHub Action to send the webhook. I recommend using [Workflow Webhook Action](https://github.com/marketplace/actions/workflow-webhook-action) or [HTTP Request Action](https://github.com/fjogeleit/http-request-action). 
7. To test this setup, you should be able to push a change to the GitHub repository, and see that change reflected on the website automatically.
8. For offline grading, add the instructor (@russfeld) to the repository as maintainers, and submit the repository and URL where the files can be found in your grading packet. Provided the webhook works correctly, they should be able to see a pushed change to the repository update the website. 

Of course, you may need to modify your firewall configuration to allow incoming connections for Webhook! **If your firewall is disabled and/or not configured, there will be a deduction of up to 10% of the total points on this lab**

{{% notice tip %}}
_Since the Webhook process runs as the `root` user on **BACKEND**, you'll need to make sure a set of SSH keys exist in the `root` user's home folder `/root/.ssh/` and add the public key from that directory to your [GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account). You should then use the root account (use `sudo su -` to log in as root) to run `git pull` from the appropriate directory on **BACKEND** at least once so you can accept the SSH fingerprint for the GitHub server. This helps ensure that `root` can properly run the script. --Russ_
{{% /notice %}}

#### Resources

* **[Extras - Git]({{% relref "/X-extras/07-git"  %}})**
* [webhook](https://github.com/adnanh/webhook) on GitHub
* [webhook Hook Examples](https://github.com/adnanh/webhook/blob/master/docs/Hook-Examples.md) on GitHub
* [GitLab Webhooks](https://docs.gitlab.com/ee/user/project/integrations/webhooks.html) on GitLab Documentation
* [GitHub Webbooks](https://docs.github.com/en/webhooks/using-webhooks/creating-webhooks) on GitHub Documentation.

---

### Task 4: Submit Files

This lab may be graded completely offline. To do this, submit the following items via Canvas:

2. **Task 1**: An archive file containing a README document as well as any files or information needed as part of the backup of the Ubuntu web application installed in Lab 6.
3. **Task 2**: The URL and password of your Checkmk instance, clearly showing data from both **FRONTEND** and **BACKEND**. 
4. **Task 3**: A GitLab/GitHub repository URL and a URL of the website containing those files. Make sure the instructor is added to the repository as maintainers. They should be able to push to the repository and automatically see the website get updated. 

If you are able to submit all 4 of the items above, you do not need to schedule a grading time. The instructor or TA will contact you for clarification if there are any questions on your submission.

For Tasks 2 - 3, you may also choose to do interactive grading, especially if you were unable to complete it and would like to receive partial credit. 

### Task 5: Schedule A Grading Time

If you are not able to submit information for all 3 tasks for offline grading, you may contact the instructor and schedule a time for interactive grading. You may continue with the next module once grading has been completed.
