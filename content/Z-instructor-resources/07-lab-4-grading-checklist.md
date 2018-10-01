---
title: "Lab 4 Grading Checklist"
weight: 35
pre: "4.1 "
---

- Install Windows Server 2016 Standard (3)
  - Static IP
  - DNS server point to itself
- Install AD DS (10)
  - Domain name: `ad<user>.cis527.cs.ksu.edu`
  - Domain user
- Windows 10 Client on AD (5)
  - Log in with domain user
- Install OpenLDAP (15)
  - Domain Name: `dc=cis527<user>,dc=local`
  - Install phpLDAPadmin
  - LDAP OUs: `users` and `groups`
  - LDAP groups: `admin`
  - LDAP user
- Ubuntu Client on LDAP (5)
  - Log in with LDAP user
- Interoperability (10)
  - Add Ubuntu to Windows AD
  - Set up Samba on Ubuntu and add Windows
- LDAPSearch (2)
  - Screenshots
