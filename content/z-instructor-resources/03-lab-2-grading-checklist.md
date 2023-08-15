---
title: "Lab 2 Grading Checklist"
weight: 15
pre: "2.1 "
---

- Windows Manifest (5)
  - Compiles
  - Runs Without Errors
  - Comments for any modules to install
- Windows Configuration (10)
  - Users (cis527, AdminUser, NormalUser, GuestUser, EvilUser)
  - Groups (Administrators, Users, Files)
  - Software (Firefox, Thunderbird, Notepad++)
- Windows Files (10)
  - Run `Get-ChildItem -Recurse | Get-Acl | Format-List`
  - Check for groups and user on each folder
- Ubuntu Manifest (5)
  - Compiles
  - Runs Without Errors
  - Comments for any modules to install
- Ubuntu Configuration (10)
  - Users (cis527, AdminUser, NormalUser, GuestUser, EvilUser)
  - Groups (files)
  - Software (Firefox, Thunderbird, Synaptic)
- Ubuntu Files (10)
  - Run `ls -lR`
  - Check for groups and user on each folder
