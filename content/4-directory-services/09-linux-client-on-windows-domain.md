---
title: "Linux Client on Windows Domain"
weight: 45
pre: "9. "
---

{{< youtube  >}}

#### Resources

* **[Slides]({{< relref "/4-directory-services/09-linux-client-on-windows-domain-slides.md" >}})**
* [Join Ubuntu 18.04 to Active Directory](https://bitsofwater.com/2018/05/08/join-ubuntu-18-04-to-active-directory/) by Michael Waterman from Bits of Water
* [Managing sudo using Active Directory](https://bitsofwater.com/2018/07/10/managing-sudo-using-active-directory/) by Michael Waterman from Bits of Water

#### Video Transcript

In the following two videos, we'll look at how to enable interoperability between our Windows- and Linux-based systems. In many organizations today, you'll have a mix of many different operating systems, so it is very helpful to understand how to integrate them together in a single directory service.

In this video, I'll show you how to add an Ubuntu VM to a Windows Active Directory Domain. This is by far the most common use-case for interoperability, and has been used by many organizations including K-State. For most users, Windows Active Directory provides a great set of features for Windows-based systems, and it is simple to integrate Linux and Mac clients into that environment.

For this example, I'm using the Windows 2016 server from the previous video. However, I've reconfigured the domain to have the fully qualified domain name `ad.cis527.cs.ksu.edu` for this example, as you would in a real environment. This is due to the fact that many Linux packages do not accept the `.local` top-level domain I used in the previous video as an example.

For the client, I have restored my Ubuntu 18.04 VM labelled **Client** to a snapshot taken before it was configured as a client for OpenLDAP. Remember that you'll need create this snapshot before you start the Lab 4 assignment, or else you may need to create a new VM for this activity.

Finally, I'll generally be following the great guide by Michael Waterman that is linked in the resources section below this video, but I'll be making a few minor changes to match our environment and clarifying a few things that he leaves out.

First, as with any client I wish to add to a domain, I'll need to set a static DNS entry to point to the domain controller itself. For the second entry, I'll just use the VMware router as always.

Then, I'll need to install several packages. These are required to use the System Security Services Daemon `sssd` as well as Kerberos for managing authentication, and the `realmd` daemon for enrolling in an Active Directory domain. Finally, we'll install some tools from Samba to enable file sharing.

```bash
sudo apt update
sudo apt install realmd sssd sssd-tools libnss-sss libpam-sss krb5-user adcli samba-common-bin
```

As you install these packages, it will ask you to enter the name of your domain and domain server. So, you'll need to enter the appropriate information there.

Next, we'll need to edit the Kerberos configuration file and add a few lines to the `[libdefaults]` section

```bash
sudo nano /etc/krb5.conf
```

Under the section labelled `[libdefaults]`, add the following two lines:

```
dns_lookup_realm = true
dns_lookup_kdc = true
```

This will instruct Kerberos to use DNS for all name lookups, which is what we'll want to use for this example.

In the guide, he also discusses configuring `timesyncd` to make sure the system's time is synchronized. However, since we are using VMware, each system's time should be synchronized with the host system's clock anyway, so this isn't necessary in our setup. On a production system, you'd definitely want to do this as well.

Next, we'll need to create a configuration file for realmd, and add some settings. First, open the file using nano:

```bash
sudo nano /etc/realmd.conf
```

Then, add this content:

```
[users]
 default-home = /home/%D/%U
 default-shell = /bin/bash

[active-directory]
 default-client = sssd
 os-name = Ubuntu Workstation
 os-version = 18.04

[service]
 automatic-install = no

[ad.cis527.cs.ksu.edu]
 fully-qualified-names = yes
 automatic-id-mapping = no
 user-principal = yes
 manage-system = yes
```

You'll need to change the domain name at the top of the fourth section to reflect your setup.

Finally, we'll need to configure the system to automatically create home directories for us. To do that, we can use this command

```
sudo pam-auth-update
```

In the menu, press the <kbd>SPACE</kbd> key to enable the "Create home directory on login" option, then press <kbd>ENTER</kdb> to save the changes.

Now, we can briefly test our connection and make sure everything is working. Make sure the Windows 2016 server is running before executing these commands. First:

```bash
realm discover ad.cis527.cs.ksu.edu
```

should tell us all about our domain we wish to connect to. Next, we can test Kerberos authentication using:

```bash
kinit Administrator
```

to get a ticket, then

```
klist
```

to view our active tickets. Finally, we must use

```
kdestroy
```

to remove the ticket before joining the domain.

Finally, we can join this computer to our Active Directory domain using the `realm join` command:

```
sudo realm join --verbose --user=Administrator ad.cis527.cs.ksu.edu
```

You should be prompted for the password for the Administrator account on the domain. Then, if all is successful, you should receive a message stating that you've joined the domain.

Lastly, before we can log in, we must make a couple of edits to the `sssd` configuration file. First, you'll need to open it

```bash
sudo nano /etc/sssd/sssd.conf
```

Then, under the section labelled `[sssd]`, add the following line

```
default_domain_suffix = ad.cis527.cs.ksu.edu
```

Of course, you'll need to edit that line to match your fully qualified domain name. Finally, toward the bottom of the file, find the line for `ldap_id_mapping` and change it to the following:

```
ldap_id_mapping = True
```

That should do it! Finally, restart your VM, and click the "Not Found" option on the login screen. Here, you can enter any username on the Active Directory Domain, followed by the password, and it should log in as that user.

As you can see, adding an Ubuntu VM to a Windows Active Directory Domain is fairly straightforward, once you have all the pieces in place. In the next video, we'll look at how to set up an Ubuntu server to act as an Active Directory Domain Controller using Samba.
