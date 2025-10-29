---
title: "Ubuntu LDAP Installation"
weight: 35
pre: "7. "
---

{{< youtube zIUDIiAMGrg >}}

<!-- TODO Update Video to use LAM -->

<!-- BFvknNpAAIM -->

{{% notice note %}}

PHPLDAPAdmin no longer works on Ubuntu 24.04 since it has several incompatibility issues with PHP 8+. The assignment has been updated to use the new LDAP Account Manager (LAM) software instead. You may ignore the part of this video showing how to configure PHPLDAPAdmin and instead refer to the guide linked from the assignment page to configure LAM.

Also, see the transcript below for an updated version of the `ldapwhoami` command. 

{{% /notice %}}

#### Resources

* [How to Install OpenLDAP on Ubuntu 22.04](https://www.howtoforge.com/how-to-install-openldap-on-ubuntu-22-04/) from HowToForge (works for Ubuntu 24.04)
  * Note: In this document, you can skip the steps of manually adding groups and users to LDAP before install LDAP Account Manager. Once LAM is configured, it will automatically add the default OUs for groups and users. 
* [LDAP & TLS](https://ubuntu.com/server/docs/ldap-and-transport-layer-security-tls) from the Ubuntu Server Guide
* [How Does HTTPS Work](https://www.youtube.com/watch?v=T4Df5_cojAs) from kubucation on YouTube (a good overview of CAs and certificates)
* **[Core Networking Services - Security]({{% relref "/3-core-networking-services/15-security"  %}})**
* **[The Cloud - Certificates]({{% relref "/5-the-cloud/06-certificates"  %}})**

#### Video Transcript

As we did earlier with setting up Active Directory on Windows, let's take a look at the steps required to install and configure OpenLDAP on Linux. The goal of this video isn't to show you all the steps of the process, but provide commentary on some of the more confusing steps you'll perform.

For this example, I'm using the Ubuntu VM labelled Server from Lab 3. I have chosen to disable the DHCP server on this system, and instead have replaced it with the VMware DHCP server. In practice, that change should not affect any of this process. Also, I'll generally be following the guide from DigitalOcean, which is linked in the resources section below the video.

At this point, I have also already performed the first steps of the guide, which is to install the `slapd` and `ldap-utils` packages on this system. Now, I'll step through the configuration process for `slapd` and discuss the various options it presents.

```bash
sudo dpkg-reconfigure slapd
```

First, it will ask you if you want to omit the OpenLDAP server configuration. Make sure you select `<No>` for that option. You can use the arrow keys (<kbd>&larr;</kbd> and <kbd>&rarr;</kbd>) to move the red-shaded selector to the option you'd like to select, then press <kbd>ENTER</kbd> to confirm it.

Next, it will ask for your domain name. For this example, I'll just use `ldap.cis527russfeld.cs.ksu.edu`. You'll need to adjust these settings to match the required configuration for the lab assignment. This matches the DNS configuration I made in Lab 3, which is very important later on in this process.

Next, it will also ask for your organization name. I'll just use `cis527` here.

Then, it will ask for your Administrator password. This is the equivalent of the `root` account within the domain. It is able to change all domain settings, and therefore the password for this account should be very complex and well protected. For this example, I'll just use the same password we are using for everything else, but in practice you'll want to carefully consider this password.

The next option is whether you want to have the database removed if you purge the `slapd` package. Selecting `<yes>` on this option would delete your LDAP database if you ever chose to reinstall the `slapd` package. For most uses, you'll always want to select `<no>` here, which is what I'll do.

Since there are some existing configuration files in place, the installer asks if you'd like those to be moved. Unless you are reinstalling `slapd` on an existing server, you can select `<yes>` for this option.

That should complete the configuration for the OpenLDAP server. For this example, I have disabled the firewall on this system, but for your lab assignment you'll need to do a bit of firewall configuration at this point.

---

<!--Next, I'm going to configure `phpldapadmin` on this server. It is a useful web interface for managing your OpenLDAP server. We can install it using `apt`:

```bash
sudo apt install phpldapadmin
```

Once it has been installed, we'll just need to configure it by editing its configuration file. 

```bash
sudo nano /etc/phpldapadmin/config.php
```

In that file, you'll need scroll down to around line 286 to find the configuration for your LDAP servers. You'll need to set the server name, host address, and login information. You can roughly follow the first guide from DigitalOcean linked below this video for these changes as well. For my system, I'll configure the following lines (you may need to uncomment some of them as well):

```php
$servers->setValue('server', 'name', 'CIS 527 LDAP');
$servers->setValue('server', 'host', '127.0.0.1');
$servers->setValue('server', 'base', array('dc=ldap,dc=cis527russfeld,dc=cs,dc=ksu,dc=edu'));
$servers->setValue('login', 'bind_id', 'cn=admin,dc=ldap,dc=cis527russfeld,dc=cs,dc=ksu,dc=edu');
```

At last, you can load the website by navigating to `http://localhost/phpldapadmin` in your web browser.

---

Once we've loaded the interface, we'll need to add a few items to make this server fully useable. The second guide linked below this video gives the steps for adding some organizational units, groups, and users to the server. I've already performed the steps to add the `users` and `groups` organizational units, as well as the `admin` group. For this video, I am going to discuss a few issues related to creating LDAP users.

To begin, I'll click on the "ou=users" link on the left, then the "Create a child entry" link on the right. I'll choose the "Generic: User Account" template next. On this page, I'll enter the information for my user account. Note that the "Common Name" field must be unique, so it is a good idea to input the user's username here, instead of the default of their first and last name. I'll leave the home directory as the default, choose the "admin" group, and the Bash login shell. Finally, I'll enter a password, and click the "Create Object" button to create it. Once it is created, I'll edit the UID number to be 10000 instead of 1000. This is very important, because by default accounts on Ubuntu start at UID 1000, so this could create a UID conflict.


--- -->

Finally, let's add some encryption to this server to protect the information shared across the network. This step was not required in previous versions of this lab, but it has always been a good idea. Now that Ubuntu uses SSSD, or System Security Services Daemon, for authentication, it requires us to provide TLS encryption on our LDAP server. So, let's do that now.

For these steps, we'll be closely following the Ubuntu Server Guide linked below this video. We'll be adjusting a few of the items to match our configuration, but most of the commands are exactly the same.

First, we'll need to install a couple of packages to allow us to create and manipulate security certificates

```bash
sudo apt update
sudo apt install gnutls-bin ssl-cert
```

Next, we need to create our own certificate authority, or CA. In a production system, you would instead work with an actual CA to obtain a security certificate from them, but that can be time consuming and expensive. So, for this example, we'll just create our own. Also, contrary to what your browser may lead you to believe, using your own CA certificates will result in an encrypted connection, it just may not be "trusted" since your browser doesn't recognize the CA certificate. 

If you want to know more about CAs and certificates, check out the handy YouTube video I've linked below this video. It gives a great description of how certificates work in much more detail. I've also included links to the lectures in Module 3 and Module 5 that deal with TLS certificates. 

So, we'll first create a private key for our CA:

```bash
sudo certtool --generate-privkey --bits 4096 --outfile /etc/ssl/private/mycakey.pem
```

Then, we'll create a template file that contains the options we need for creating this certificate. Notice here that I've modified this information from what is provided in the Ubuntu Server Guide document to match our setup:

```bash
sudo nano /etc/ssl/ca.info
```

and put the following text into that file. 

```tex
cn = CIS 527
ca
cert_signing_key
expiration_days = 3650
```

Then, we can use that template to create our self-signed certificate authority certificate:

```bash
sudo certtool --generate-self-signed --load-privkey /etc/ssl/private/mycakey.pem --template /etc/ssl/ca.info --outfile /usr/local/share/ca-certificates/mycacert.crt
```

This will create a certificate called `mycacert.crt` that is stored in `/usr/local/share/ca-certificates/`. **This is our self-signed CA certificate**. So, whenever we want any system to trust one of our self-signed certificates that we make from our CA, we'll need to make sure that system has a copy of this CA certificate in its list of trusted certificates. 

To do that, we simply place the certificate in `/usr/local/share/ca-certificates/`, and then run the following command to add it to the list of trusted certificates:

```bash
sudo update-ca-certificates
```

If that command works correctly, it should tell us that it has added 1 certificate to our list. 

Before we move on, let's make a copy of our `mycacert.crt` file in our `cis527` users's home directory. We'll use this file in the next part of this lab when we are configuring our client system to authenticate using LDAP. 

```bash
cp /usr/local/share/ca-certificates/mycacert.crt ~/
```

Now that we've created our own self-signed CA, we can use it to create a certificate for our LDAP server. So, we'll start by creating yet another private key:

```bash
sudo certtool --generate-privkey --bits 2048 --outfile /etc/ldap/ldap01_slapd_key.pem
```

Then, we'll create another template file to give the information about the certificate that we'd like to create:

```bash
sudo nano /etc/ssl/ldap01.info
```

and place the following tex in that file:

```tex
organization = CIS 527
cn = ldap.cis527russfeld.cs.ksu.edu
tls_www_server
encryption_key
signing_key
expiration_days = 365
```

Notice that in that file, we entered the fully qualified domain name for our LDAP server on the second line. This is the most important part that makes all of this work. On our client machine, we must have a DNS entry that links this domain name to our LDAP server's IP address, and then the certificate the server uses must match that domain name. So, if we don't get this step right, the whole system may not work correctly until we fix it!

Finally, we can use this long and complex command to create and sign our server's certificate:

```bash
sudo certtool --generate-certificate --load-privkey /etc/ldap/ldap01_slapd_key.pem --load-ca-certificate /etc/ssl/certs/mycacert.pem --load-ca-privkey /etc/ssl/private/mycakey.pem --template /etc/ssl/ldap01.info --outfile /etc/ldap/ldap01_slapd_cert.pem
```

Once the certificate has been created, we just need to do a couple of tweaks so that it has the correct permissions. This will allow the LDAP server to properly access the file:

```bash
sudo chgrp openldap /etc/ldap/ldap01_slapd_key.pem
sudo chmod 0640 /etc/ldap/ldap01_slapd_key.pem
```

Finally, at long last, we are ready to tell our LDAP server to use the certificate. To do that, we'll create an LDIF file:

```bash
nano ~/certinfo.ldif
```

and in that file we'll put the information about our certificate:

```tex
dn: cn=config
add: olcTLSCACertificateFile
olcTLSCACertificateFile: /etc/ssl/certs/mycacert.pem
-
add: olcTLSCertificateFile
olcTLSCertificateFile: /etc/ldap/ldap01_slapd_cert.pem
-
add: olcTLSCertificateKeyFile
olcTLSCertificateKeyFile: /etc/ldap/ldap01_slapd_key.pem
```

Once that file is created, we can use the `ldapmodify` tool to import it into our server:

```bash
sudo ldapmodify -Y EXTERNAL -H ldapi:/// -f certinfo.ldif
```

Whew! That was a lot of work! Now, if we did everything correctly, we should be able to query this LDAP server using TLS. The best way to check that is by using the following command:

```bash
ldapwhoami -x -ZZ -H ldap.cis527russfeld.cs.ksu.edu
```

The `-ZZ` part of that command tells it to use TLS, and if it works correctly it should return `anonymous` as the result. If this step fails, then you may need to do some troubleshooting to see what the problem is. 

That should do it! In the next video, I'll show how to configure another Ubuntu VM to use this LDAP server for authentication.
