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
  - Domain Name: `dc=ldap,dc=cis527<eID>,dc=cs,dc=ksu,dc=edu`
  - Install phpLDAPadmin
  - LDAP OUs: `users` and `groups`
  - LDAP groups: `admin`
  - LDAP user
  - TLS (test client side with `ldapwhoami -x -Z ldap.cis527<eID>.cs.ksu.edu` returning `anonymous`
- Ubuntu Client on LDAP (5)
  - Log in with LDAP user
- Interoperability (10)
  - Add Ubuntu to Windows AD

- LDAPSearch (2)
  - Screenshots
