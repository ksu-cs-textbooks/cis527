---
title: "Assignment"
weight: 25
pre: "5. "
---

### Lab 3 - Core Networking Services

#### Instructions

Create **three** virtual machines meeting the specifications given below. The best way to accomplish this is to treat this assignment like a checklist and check things off as you complete them.

If you have any questions about these items or are unsure what they mean, please contact the instructor. Remember that part of being a system administrator (and a software developer in general) is working within vague specifications to provide what your client is requesting, so eliciting additional information is a very necessary skill.

{{% notice note %}}
_To be more blunt - this specification may be purposefully designed to be vague, and it is your responsibility to ask questions about any vagaries you find. Once you begin the grading process, you cannot go back and change things, so be sure that your machines meet the expected specification regardless of what is written here. --Russ_
{{% /notice %}}

Also, to complete many of these items, you may need to refer to additional materials and references not included in this document. System administrators must learn how to make use of available resources, so this is a good first step toward that. Of course, there's always [Google](http://www.google.com)!

#### Time Expectation

This lab may take anywhere from **1 - 6 hours** to complete, depending on your previous experience working with these tools and the speed of the hardware you are using. Installing virtual machines and operating systems is very time-consuming the first time through the process, but it will be much more familiar by the end of this course.

---

### Task 0: Create 3 VMs

For this lab, you'll need to have **ONE Windows 10 VM**, and **TWO Ubuntu 20.04 VMs** available. You may reuse existing VMs from Lab 1 or Lab 2. In either case, they should have the full expected configuration applied, either manually as in Lab 1 or via the Puppet Manifest files created for Lab 2.

For the second Ubuntu VM, you may either quickly install and configure a new VM from scratch following the Lab 1 guide or using the Puppet Manifest from Lab 2, or you may choose to create a copy of one of your existing Ubuntu VMs. If you choose to copy one, follow these steps:

1. Completely shut down the VM - do not suspend it.
2. Close VMware Workstation.
3. Make a copy of the entire folder containing the VM.
4. Open the new VM in VMware Workstation (look for the .VMX file in the copied folder).
5. When prompted, select "I copied it" to reinitialize the network interface. **THIS IS IMPORTANT!**
6. Boot the new VM, and change the hostname to `cis527s-<your eID>`.
   - [How to Change Hostname on Ubuntu 20.04](https://linuxconfig.org/how-to-change-hostname-on-ubuntu-20-04-focal-fossa-linux) from LinuxConfig.org

{{% notice warning %}}
_If you do not follow these instructions carefully, the two VMs may have conflicts on the network since they'll have identical networking hardware and names, making this lab much more difficult or impossible to complete. **You have been warned!** --Russ_
{{% /notice %}}

Clearly label your original Ubuntu VM as **CLIENT** and the new Ubuntu VM as **SERVER** in VMware Workstation so you know which is which. For this lab, we'll mostly be using the **SERVER** VM, but will use the **CLIENT** VM for some testing and as part of the SNMP example in Task 5. 

{{% notice note %}}
**VMware Fusion (Mac) Users** - Before progressing any further, I recommend creating a new NAT virtual network configuration and moving all of your VMs to that network, instead of the default "Share with my Mac" (vmnet8) network. In this lab, you'll need to disable DHCP on the network you are using, which is very difficult to do on the default networks. You can find relevant instructions in [Add a NAT Configuration](https://docs.vmware.com/en/VMware-Fusion/8.0/com.vmware.fusion.using.doc/GUID-7D8E5A7D-FF0C-4975-A794-FF5A9AE83234.html) and [Connect and Set Up the Network Adapter](https://docs.vmware.com/en/VMware-Fusion/8.0/com.vmware.fusion.using.doc/GUID-84AC2D7D-4A44-4AB6-BAF8-F12C55E71A2F.html) in the VMware Fusion 8 Documentation.
{{% /notice %}}

---

### Task 1: Remote Connections

**PART A:** On your Windows 10 VM, activate the **Remote Desktop** feature to allow remote access.

* Both the `cis527` and `AdminUser` accounts should be able to access the system remotely, as well as the default system `Administrator` account.
* In addition, **change the port** used by Remote Desktop to be 34567.
{{% notice tip %}}
_You'll need to edit the registry and reboot the computer to accomplish this task. --Russ_
{{% /notice %}}
* You'll also need to make sure appropriate firewall rules are in place to accept these incoming connections, and ensure the firewall is properly enabled.
* You can test your connection from your Linux VM using the **Remmina** program.

**PART B:** On your Ubuntu 20.04 VM labelled **SERVER**, install and activate the **OpenSSH Server** for remote access.

* Both the `cis527` and `AdminUser` accounts should be able to access the system remotely.
* In addition, **change the port** used by the SSH server to 23456.
* You'll also need to make sure the appropriate firewall rules are in place to accept these incoming connections, and ensure the firewall is properly enabled.
* You can test your connection from your Windows VM using [PuTTY](http://putty.org) or the Windows Subsystem for Linux, or from the Ubuntu 20.04 VM labelled **CLIENT** using the `ssh` command.
{{% notice tip %}}
_See the appropriate pages in the Extras module for more information about WSL and SSH. --Russ_
{{% /notice %}}

#### Resources

* [How to Set Up and Use Remote Desktop for Windows 10](https://www.groovypost.com/howto/setup-use-remote-desktop-windows-10/) from groovyPost
* [How to Change the Listening Port for Remote Desktop](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/change-listening-port) from Microsoft Support
* [Change Remote Desktop RDP Port](https://tweaks.com/windows/50743/change-remote-desktop-rdp-port/) from Tweaks.com
* [OpenSSH Server](https://ubuntu.com/server/docs/service-openssh) from the Ubuntu Server Guide
* [Configuring OpenSSH](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring) from Ubuntu Community Help Wiki
* [Ubuntu 20.04 SSH Server](https://linuxconfig.org/ubuntu-20-04-ssh-server) from LinuxConfig.org

---

### Task 2: Ubuntu Static IP Address

On your Ubuntu 20.04 VM labelled **SERVER**, set up a static IP address. The host part of the IP address should end in `.41`, and the network part should remain the same as the one automatically assigned by VMware.

{{% notice note %}}
So, if your VMware is configured to give IP addresses in the `192.168.138.0/24` network, you'll set the computer to use the `192.168.138.41` address.
{{% /notice %}}

You'll need to set the following settings correctly:

* IP Address
* Subnet Mask
* Default Gateway
{{% notice note %}}
VMware typically uses host `2` as its internal router to avoid conflicts with home routers, which are typically on host `1`. So, on the `192.168.138.0/24` network, the default gateway would usually be `192.168.138.2`. When in doubt, you may want to record these settings on one of your working VMs before changing them. 
{{% /notice %}}
* DNS Servers. Use one of the following options:
  - Your Default Gateway Address (easiest). VMware's internal router also acts as a DNS resolver for you, just like a home router would
  - Off Campus: [OpenDNS](https://www.opendns.com/setupguide/) (`208.67.222.222` and `208.67.220.220`) or [Google DNS](https://developers.google.com/speed/public-dns/) (`8.8.8.8` and `8.8.4.4`)
  - On Campus: [K-State's DNS Servers](https://www.k-state.edu/its/dns/registration.html) (`10.130.30.52` and `10.130.30.53`)

{{% notice tip %}}
_I personally recommend using the graphical tools in Ubuntu to configure a static IP address. There are many resources online that direct you to use netplan or edit configuration files manually, but I've found that those methods aren't as simple and many times lead to an unusable system if done incorrectly. In any case, **making a snapshot before this step** is recommended, in case you have issues. --Russ_
{{% /notice %}}

#### Resources

* [How to Configure Static IP Address on Ubuntu 20.04 Focal Fossa Desktop/Server](https://linuxconfig.org/how-to-configure-static-ip-address-on-ubuntu-20-04-focal-fossa-desktop-server) from LinuxConfig.org
* [How to Configure Static IP Address on Ubuntu 18.04](https://linoxide.com/linux-how-to/configure-static-ip-address-ubuntu/) from LinOxide (should work for 20.04 as well)
* _The Command Line Way: [Network Configuration](https://ubuntu.com/server/docs/network-configuration) from Ubuntu Server Guide._

---

### Task 3: DNS Server

For this step, install the `bind9` package on the Ubuntu 20.04 VM labelled **SERVER**, and configure it to act as a **primary master** and **caching nameserver** for your network. You'll need to include the configuration for both types of uses in your config file. In addition, you'll need to configure both the **zone file** and **reverse zone file**, as well as **forwarders**.

{{% notice tip %}}
_These instructions were built based on the [How To Configure BIND as a Private Network DNS Server on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-configure-bind-as-a-private-network-dns-server-on-ubuntu-18-04) guide from DigitalOcean. In general, you can follow the first part of that guide to configure a Primary DNS Server, making the necessary substitutions listed below. The directions are basically the same for Ubuntu 20.04. --Russ_
{{% /notice %}}

In your configuration, include the following items:

* All files:
  * On Ubuntu 20.04, the location of the default settings file has moved from `/etc/default/bind9` to `/etc/default/named`
  * Since you are not creating a Secondary DNS Server, you can leave out any `allow-transfer` entries from all configuration files.
* `named.conf.options` file:
  * Create an ACL called `cis527` that includes your entire VM network in CIDR notation. Do not list individual IP addresses.
  * Enable recursion, and allow all computers in the `cis527` ACL to perform recursive queries.
  * Configure DNS forwarding, using one of the options given above in Task 2. I recommend using the same option as above, since you have (_hopefully_) already confirmed that it works for your situation.
* `named.conf.local` file:
  * Create a zone file and reverse zone file, stored in `/etc/bind/zones`.
{{% notice note %}}
The DigitalOcean guide uses a `/16` subnet of `10.128.0.0/16`, and includes the `10.128` portion in the reverse zone file name and configuration. For your VM network, you are most likely using a `/24` subnet, such as `192.168.40.0/24`, so you can include the `192.168.40` portion in your zone file name and configuration. In that case, the zone name would be `40.168.192.in-addr.arpa`, and the file could be named accordingly. Similarly, in the reverse zone file itself, you would only need to include the last segment of the IP address for each PTR record, instead of the last two. Either way is correct.
{{% /notice %}}
  * List those files by path in this file in the correct zone definitions.
* Zone files:
  * Use `<your eID>.cis527.cs.ksu.edu` as your fully qualified domain name (FQDN) in your configuration file. (Example: `russfeld.cis527.cs.ksu.edu`)
  * Use `ns.<your eID>.cis527.cs.ksu.edu` as the name of your authoritative nameserver. You can use `admin.<your eID>.cis527.cs.ksu.edu` for the contact email address.
{{% notice note %}}
Since the at symbol `@` has other uses in the DNS Zone file, the email address uses a period `.` instead. So, the email address `admin@<your eID>.cis527.cs.ksu.edu` would be written as `admin.<your eID>.cis527.cs.ksu.edu`.
{{% /notice %}}
  * Don't forget to increment the `serial` field in the `SOA` record each time you edit the file. Otherwise your changes may not take effect.
  * Create an NS record for `ns.<your eID>.cis527.cs.ksu.edu`.
{{% notice tip %}}
_HINT: The DigitalOcean guide does not include an at symbol `@` at the beginning of that record, but I've found that sometimes it is necessary to include it in order to make the `named-checkzone` command happy. See a related post on [ServerFault](https://serverfault.com/questions/802762/reverse-dns-bind-named-checkzone-zone-ns-has-no-address-records-a-or-aaaa-err) for additional ways to solve that common error.--Russ_
{{% /notice %}}
* Forward Zone File:
  * Create an A record for `ns.<your eID>.cis527.cs.ksu.edu` that points to your Ubuntu 20.04 VM labelled **SERVER** using the IP address in your network ending in `41` as described above.
  * Create an A record for `windows.<your eID>.cis527.cs.ksu.edu` that points to the IP address in your network ending in `42`. _(You'll use that IP address in the next assignment for your Windows server.)_
  * Create an A record for `ldap.<your eID>.cis527.cs.ksu.edu` that points to your Ubuntu 20.04 VM labelled **SERVER** using the IP address in your network ending in `41` as described above. This record will be for the LDAP server in Lab 4.
  * Create an A record for `ad.<your eID>.cis527.cs.ksu.edu` that points to the IP address in your network ending in `42`. _(You'll use that IP address in the next assignment for your Windows server.)_ This record will be for the Active Directory server in Lab 4
  * Create a CNAME record for `ubuntu.<your eID>.cis527.cs.ksu.edu` that redirects to `ns.<your eID>.cis527.cs.ksu.edu`.
* Reverse Zone File:
  * Create a PTR record for the IP address ending in `41` that points to `ns.<your eID>.cis527.cs.ksu.edu`.
  * Create a PTR record for the IP address ending in `42` that points to `windows.<your eID>.cis527.cs.ksu.edu`.


{{% notice tip %}}
_HINT: The periods, semicolons, and whitespace in the DNS configuration files are very important! Be very careful about formatting, including the trailing periods after full DNS names such as `win.<your eID>.cis527.ksu.edu.`. --Russ_
{{% /notice %}}

Once you are done, I recommend checking your configuration using the `named-checkconf` and `named-checkzone` commands. Note that the second argument to the `named-checkzone` command is the full path to your zone file, so you may need to include the file path and not just the name of the file. Example: `named-checkzone russfeld.cis527.cs.ksu.edu /etc/bind/zones/db.russfeld.cis527.cs.ksu.edu`

Of course, you may need to update your firewall configuration to allow incoming DNS requests to this system! **If your firewall is disabled and/or not configured, there will be a deduction of up to 10% of the total points on this lab**

To test your DNS server, you can set a static DNS address on either your Windows or Ubuntu VM labelled **CLIENT**, and use the `dig` or `nslookup` commands to verify that each DNS name and IP address is resolved properly.

{{% notice note %}}
See the [Bind Troubleshooting]({{< relref "/3-core-networking-services/17-bind-troubleshooting.md" >}}) page for some helpful screenshots of using `dig` to debug DNS server configuration. 
{{% /notice %}}

#### Resources

* [How To Configure BIND as a Private Network DNS Server on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-configure-bind-as-a-private-network-dns-server-on-ubuntu-18-04) from DigitalOcean (works for 20.04 as well)
* [Bind9 Server How-To](https://help.ubuntu.com/community/BIND9ServerHowto) from Ubuntu Community Help Wiki
* [DNS Configuration](https://ubuntu.com/server/docs/service-domain-name-service-dns) from Ubuntu Server Guide
* [BIND Manuals](http://www.bind9.net/manuals) from bind9.net
* [Reverse DNS/bind named-checkzone "zone NS has no address records (A or AAAA) error"](https://serverfault.com/questions/802762/reverse-dns-bind-named-checkzone-zone-ns-has-no-address-records-a-or-aaaa-err) on ServerFault (_common error in previous semesters_)

---

### Task 4: DHCP Server

{{% notice warning %}}
_**IMPORTANT!** Make ABSOLUTELY sure that the VMware virtual network you are using is not a "Bridged" or "Shared" network before continuing. It **MUST** be using "NAT". You can check by going to **Edit > Virtual Network Editor** in VMware Workstation or **VMware Fusion > Preferences > Network** in VMware Fusion and looking for the settings of the network each of your VMs is configured to use. Having your network configured incorrectly while performing this step is a great way to break the network your host computer is currently connected to, and in a worst case scenario will earn you a visit from K-State's IT staff (and they won't be happy)! --Russ_
{{% /notice %}}

Next, install the `isc-dhcp-server` package on the Ubuntu 20.04 VM labelled **SERVER**, and configure it to act as a DHCP server for your internal VM network.

In your configuration, include the following items:

* In general, the network settings used by this DHCP server should match those used by VMware's internal router.
  - You can also look at the network settings received by your Windows 10 VM, which at this point are from VMware's internal router.
* Use `<your eID>.cis527.cs.ksu.edu` as the domain name. (Example: `russfeld.cis527.cs.ksu.edu`)
* For the dynamic IP range, use IPs ending in `.100`-`.250` in your network.
* For DNS servers, enter the **IP address** of your Ubuntu 20.04 VM labelled **SERVER** ending in `.41`. This will direct all DHCP clients to use the DNS server configured in Task 3.
  - Do not use the domain name of your DNS server in your DHCP config file. While it _can_ work, it depends on your DNS server being properly configured in Task 3. 
  - Alternatively, for testing if your DNS server is not working properly, you can use one of the other DNS options given above in Task 2. However, you must be using the DNS server from Task 3 when graded for full credit.

{{% notice tip %}}
_A working solution can be fewer than 20 lines of actual settings (not including comments) in the settings file. If you find that your configuration is becoming much longer than that, you are probably making it too difficult and complex. --Russ_
{{% /notice %}}

Of course, you may need to update your firewall configuration to allow incoming DHCP requests to this system! **If your firewall is disabled and/or not configured, there will be a deduction of up to 10% of the total points on this lab**

Once your DHCP server is installed, configured, and running properly, turn off the DHCP server in VMware. Go to **Edit > Virtual Network Editor** in VMware Workstation or **VMware Fusion > Preferences > Network** in VMware Fusion and look for the NAT network you are using. There should be an option to disable the DHCP server for that network there.

Once that is complete, you can test the DHCP server using the Windows VM. To do so, restart your Windows VM so it will completely forget any current DHCP settings. When it reboots, if everything works correctly, it should get an IP address and network information from your DHCP server configured in this step. It should also be able to access the internet with those settings. An easy way to check is to run the command `ipconfig` in PowerShell and look for the DNS suffix of `<your eID>.cis527.cs.ksu.edu` in the output. 

#### Resources

* [Dynamic Host Configuration Protocol (DHCP)](https://ubuntu.com/server/docs/network-dhcp) from Ubuntu Server Guide
* [How to Install DHCP Server in Ubuntu & Debian](https://tecadmin.net/install-dhcp-server-in-ubuntu/) from TecAdmin.net

---

### Task 5: SNMP Daemon

Install an SNMP Daemon on the Ubuntu 20.04 VM labelled **SERVER**, and connect to it from your Ubuntu 20.04 VM labelled **CLIENT**. The DigitalOcean tutorial linked below is a very good resource to follow for this part of the assignment. In that tutorial, the **agent server** will be your **SERVER** VM, and the **manager server** will be your **CLIENT** VM.

1. In the tutorial, configure a user `cis527` using the password `cis527_snmp` for both the authentication and encryption passphrases. 
   - This user **should not** be created in the `snmpd.conf` file, and any "bootstrap" users should be removed. 

{{% notice warning %}}

There is currently an issue using the `snmpusm` command to set passwords as shown in the DigitalOcean guide. I believe it is a known and unfixed bug in `snmp` itself. So, you may instead follow the steps in the "Configure SNMP Version 3 on Ubuntu 20.04" portion of the Kifarunix guide linked below to create the `cis527` user. You'll need to install the `libsnmp-dev` package, and make sure you stop the `snmpd` daemon before creating the account using the `net-snmp-create-v3-user` command. Unfortunately, when creating an account using this method, I was unable to use stored credentials on my **CLIENT** VM using a configuration file as shown in the DigitalOcean guide. When typing the full command, it did work correctly. I am not sure why that does not work - bug bounty point are available for anyone who does get it to work!

{{% /notice %}}

Of course, you may need to update your firewall configuration to allow incoming SNMP requests to this system! **If your firewall is disabled and/or not configured, there will be a deduction of up to 10% of the total points on this lab**

Then, perform the following quick activity:

1. While logged into the **CLIENT** VM, use the SNMP tools to query the number of ICMP Echos (pings) that have been received by the **SERVER** VM. Take a **screenshot** with the command used and the result clearly highlighted in the terminal output.
   - You may use either `snmpget` and the OID number or name, or use `snmpwalk` and `grep` to find the requested information. 
2. Sent at least 10 ICMP Echos (pings) from the **CLIENT** VM to the **SERVER** VM and make sure they were properly received. Take a **screenshot** of the output, clearly showing how many pings were sent.
   - If they weren't received, check your firewall settings. 
3. Once again, use the SNMP tools from the **CLIENT** VM to query the number of ICMP Echos (pings) that have been received by the **SERVER** VM. It should clearly show that it has increased by the number sent during the previous command. Take a **screenshot** with the command used and the result clearly highlighted in the terminal output. It should match the expected output based on the previous two screenshots.

{{% notice note%}}
_Be prepared to duplicate this activity during the interactive grading process! If you are unable to duplicate it, you can present the screenshots as proof that it worked before for partial credit. You may preform all three commands in a single screenshot if desired. See [this example](../../images/lab3-hint.png) for an idea of what the output should look like. --Russ_
{{% /notice %}}

#### Resources

* [How to Install and Configure an SNMP Daemon and Client on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-an-snmp-daemon-and-client-on-ubuntu-18-04) from DigitalOcean (works for 20.04 as well)
* [Quick Way to Install and Configure SNMP on Ubuntu 20.04](https://kifarunix.com/quick-way-to-install-and-configure-snmp-on-ubuntu-20-04/) from Kifarunix (includes correct command to create user accounts)
* [How to Use The Net-SNMP Tool Suite to Manage and Monitor Servers](https://www.digitalocean.com/community/tutorials/how-to-use-the-net-snmp-tool-suite-to-manage-and-monitor-servers) from DigitalOcean (works for 20.04)
* [SNMP Agent](https://help.ubuntu.com/community/SNMPAgent) from Ubuntu Community Help Wiki

---

### Task 6: Wireshark

Install Wireshark on the Ubuntu 20.04 VM labelled **SERVER**.  

{{% notice warning %}}
Firefox recently released an update the enables [DNS over HTTPS](https://hacks.mozilla.org/2018/05/a-cartoon-intro-to-dns-over-https/) by default. So, in order to use Firefox to request DNS packets that can be captured, you'll need to [disable DNS over HTTPS](https://support.mozilla.org/en-US/kb/firefox-dns-over-https) in Firefox. Alternatively, you can use `dig` to query DNS and capture the desired packets - this seems to be much easier to replicate easily. 
{{% /notice %}}

Then, using Wireshark, create **screenshots** showing that you captured and can show the packet content of each of the following types of packets:

1. A DNS standard query for an A record for `people.cs.ksu.edu`
1. A DNS standard query response for `people.cs.ksu.edu`
   * _HINT: It should respond with a CNAME record pointing to `invicta.cs.ksu.edu`_
1. A DNS standard query response for a PTR record for `208.67.222.222` (it will look like `222.222.67.208.in-addr.arpa`)
   * _HINT: It should respond with a PTR record for `resolver1.opendns.com`_
1. An ICMP Echo (ping) request
1. An encrypted SNMP packet showing `cis527` or `bootstrap` as the username (look for the `msgUserName` field)
   * _HINT: Use the commands from Task 5_
1. A DHCP Offer packet showing the Domain Name of `<your ID>.cis527.cs.ksu.edu`
   * _HINT: Reboot one of your other VMs to force it to request a new IP address, or use the `ipconfig` (Windows) or `dhclient` (Ubuntu) commands to renew the IP address_
1. An HTTP 301: Moved Permanently redirect response
   * _HINT: Clear the cache in your web browser, then navigate to `http://people.cs.ksu.edu/~sgsax` (without a trailing slash). It should redirect to `http://people.cs.ksu.edu/~sgsax/` (with a trailing slash)._
1. ~~An HTTP Basic Authentication request, **clearly showing the username and password in plaintext** (expand the entries in the middle pane to find it)~~ _This is not working due to a recent reconfiguration of the CS web server. So, this one is a freebie for now! -Russ_
   * ~~*HINT: Visit `http://people.cs.ksu.edu/~russfeld/test/` and use `cis527` | `cis527_apache` to log in*~~

{{% notice tip%}}
_You'll present those 8 screenshots as part of the grading process for this lab, so I recommend storing them on the desktop of that VM so they are easy to find. Make sure your screenshot clearly shows the data requested. --Russ_
{{% /notice %}}

#### Resources

* [Install and Use Wireshark on Ubuntu Linux](https://itsfoss.com/install-wireshark-ubuntu/) from It's FOSS

---

### Task 7: Make Snapshots

In each of the virtual machines created above, create a snapshot labelled "Lab 3 Submit" before you submit the assignment. The grading process may require making changes to the VMs, so this gives you a restore point before grading starts.

### Task 8: Schedule A Grading Time

Contact the instructor and schedule a time for interactive grading. You may continue with the next module once grading has been completed.
