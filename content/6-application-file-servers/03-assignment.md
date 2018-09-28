---
title: "Assignment"
weight: 15
pre: "3. "
---

### Lab 5 - The Cloud

#### Instructions

Create **two** cloud systems and **two** virtual machines meeting the specifications given below. The best way to accomplish this is to treat this assignment like a checklist and check things off as you complete them.

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

---

### Task 1: Windows File Server

Configure a file server on your Windows Server 2016 VM. It should have the following features:

* A shared folder on the server named `Shared` and stored at `C:\shared` that should be accessible by all users on your domain
* A shared folder on the server named `Restricted` and stored at `C:\restricted` that should only be accessible to users in the Domain Admins group in your domain

### Task 2: Windows Group Policy

Configure group policies on your Windows Active Directory domain to perform the following tasks:

* All domain users should get the

### Task 3: Ubuntu File Server

### Task 4: Ubuntu Drive Mapping

### Task 5: Windows Web Application Server

### Task 6: Ubuntu Web Application Server
