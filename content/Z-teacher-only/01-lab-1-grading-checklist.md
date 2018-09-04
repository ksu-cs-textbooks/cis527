---
title: "Lab 1 Grading Checklist"
weight: 5
pre: "1. "
---

- Install VMWare (2)
- Create Windows 10 VM (3)
  - Install VMWare (2)
  - RAM 2 GB
- Configure Windows 10 (10)
  - Computer Name
  - Users (cis527, AdminUser, NormalUser, GuestUser, EvilUser)
  - Groups (Administrators, Users, Files)
  - Software (VMWare Tools, Firefox, Thunderbird, Notepad++, BGInfo)
  - Windows Updates
  - Access IIS from Ubuntu (firewall and IIS config)
- Windows 10 Files (10)
  - Run Get-ChildItem -Recurse | Get-Acl | Format-List
  - Check for groups and user on each folder
- Create Ubuntu VM (3)
  - RAM 1 or 2 GB
- Configure Ubuntu (10)
  - Computer Name (terminal)
  - User Accounts (cat /etc/passwd)
  - Groups (cat /etc/group)
  - Software (vm tools, Synaptic, GUFW, Conky, ClamAV)
  - Firewall (enabled?)
  - Access Apache from Windows (firewall and Apache config)
  - Updates (apt update & apt upgrade)
  - Configure Automatic Updates
- Ubuntu Files (10)
  - Run ls -lR
  - Check for group and user on each folder
- Snapshots (2)
  - Windows
  - Ubuntu
