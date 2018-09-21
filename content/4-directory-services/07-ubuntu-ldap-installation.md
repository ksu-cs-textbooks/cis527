---
title: "Ubuntu LDAP Installation"
weight: 35
pre: "7. "
---

{{< youtube BFvknNpAAIM >}}

#### Resources

* [How To Install and Configure OpenLDAP and phpLDAPadmin on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-openldap-and-phpldapadmin-on-ubuntu-16-04) from DigitalOcean (works for 18.04 as well)
* [Add Organizational Units, Groups and Users](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-a-basic-ldap-server-on-an-ubuntu-12-04-vps#add-organizational-units-groups-and-users) from DigitalOcean

#### Video Transcript

As we did earlier with setting up Active Directory on Windows, let's take a look at the steps required to install and configure OpenLDAP on Linux. The goal of this video isn't to show you all the steps of the process, but provide commentary on some of the more confusing steps you'll perform.

For this example, I'm using the Ubuntu VM labelled Server from Lab 3. I have chosen to disable the DHCP server on this system, and instead have replaced it with the VMware DHCP server. In practice, that change should not affect any of this process. Also, I'll generally be following the guide from DigitalOcean, which is linked in the resources section below the video.

At this point, I have also already performed the first steps of the guide, which is to install the `slapd` and `ldap-utils` packages on this system. Now, I'll step through the configuration process for `slapd` and discuss the various options it presents.

```bash
sudo dpkg-reconfigure slapd
```

First, it will ask you if you want to omit the OpenLDAP server configuration. Make sure you select `<No>` for that option. You can use the arrow keys (<kbd>&larr;</kbd> and <kbd>&rarr;</kbd>) to move the red-shaded selector to the option you'd like to select, then press <kbd>ENTER</kbd> to confirm it.

Next, it will ask for your domain name. For this example, I'll just use `cis527.local`. You'll need to adjust these settings to match the required configuration for the lab assignment. By using a `.local` top-level domain, we can guarantee that this will never be routable on the global internet. The use of a `.local` suffix here doesn't actually comply with current DNS standards, but for our internal VM network it will work just fine. Of course, if you are doing this on an actual enterprise system, you may actually use your company's internet domain name here, with a custom prefix for your directory. For example, the K-State Computer Science department might use a domain name of `ldap.cs.ksu.edu` for this server.

Next, it will also ask for your organization name. I'll just use `cis527` here.

Then, it will ask for your Administrator password. This is the equivalent of the `root` account within the domain. It is able to change all domain settings, and therefore the password for this account should be very complex and well protected. For this example, I'll just use the same password we are using for everything else, but in practice you'll want to carefully consider this password.

Following that, it will ask what database format you'd like to use. This would allow you to use older database formats if you so choose, but in this case, we'll just select `MDB`, which is the most recent.

The next option is whether you want to have the database removed if you purge the `slapd` package. Selecting `<yes>` on this option would delete your LDAP database if you ever chose to reinstall the `slapd` package. For most uses, you'll always want to select `<no>` here, which is what I'll do.

Since there are some existing configuration files in place, the installer asks if you'd like those to be moved. Unless you are reinstalling `slapd` on an existing server, you can select `<yes>` for this option.

That should complete the configuration for the OpenLDAP server. For this example, I have disabled the firewall on this system, but for your lab assignment you'll need to do a bit of firewall configuration at this point.

---

Next, I'm going to configure `phpldapadmin` on this server. It is a useful web interface for managing your OpenLDAP server. Unfortunately, the officially available packages for Ubuntu 18.04 don't properly support PHP 7.2, which is the currently supported version. So, we're going to install a fork from GitHub that has been properly patched to support the latest version.

First, we'll need to install `git` as well as the existing version of `phpldapadmin`:

```bash
sudo apt install phpldapadmin git
```

Even though we aren't using that version of phpLDAPadmin, it helpfully installs all of the required Apache and PHP modules needed for that software. It is a nice shortcut for us. However, I'm going to disable it using these commands:

```bash
sudo a2disconf phpldapadmin
sudo systemctl reload apache
```

Next, we'll get a copy of the updated version of phpLDAPadmin using git:

```bash
cd /var/www/html
sudo git clone https://github.com/breisig/phpLDAPadmin.git phpldapadmin
```

Then, I'll need to make a copy of the default configuration file, and then edit it:

```bash
sudo cp /var/www/html/phpldapadmin/config/config.php.example /var/www/html/phpldapadmin/config/config.php
sudo nano /var/www/html/phpldapadmin/config/config.php
```

In that file, you'll need scroll down to around line 286 to find the configuration for your LDAP servers. You'll need to set the server name, host address, and login information. You can roughly follow the first guide from DigitalOcean linked below this video for these changes as well. For my system, I'll configure the following lines (you may need to uncomment some of them as well):

```php
$servers->setValue('server', 'name', 'CIS 527 LDAP');
$servers->setValue('server', 'host', '127.0.0.1');
$servers->setValue('server', 'base', array('dc=cis527,dc=local'));
$servers->setValue('login', 'bind_id', 'cn=admin,dc=cis527,dc=local');
```

Finally, we'll need to uncomment one line and set it to `true` to suppress some annoying template warnings. Here is what the website looks like with those warnings still enabled. As you can see, they are quite obtrusive. You'll find the relevant line around line 161 in the same file:

```php
$config->custom->appearance['hide_template_warning'] = true
```

At last, you can load the website by navigating to `http://localhost/phpldapadmin` in your web browser.

---

Once we've loaded the interface, we'll need to add a few items to make this server fully useable. The second guide linked below this video gives the steps for adding some organizational units, groups, and users to the server. I've already performed the steps to add the `users` and `groups` organizational units, as well as the `admin` group. For this video, I am going to discuss a few issues related to creating LDAP users.

To begin, I'll click on the "ou=users" link on the left, then the "Create a child entry" link on the right. I'll choose the "Generic: User Account" template next. On this page, I'll enter the information for my user account. Note that the "Common Name" field must be unique, so it is a good idea to input the user's username here, instead of the default of their first and last name. I'll leave the home directory as the default, choose the "admin" group, and the Bash login shell. Finally, I'll enter a password, and click the "Create Object" button to create it. Once it is created, I'll edit the UID number to be 10000 instead of 1000. This is very important, because by default accounts on Ubuntu start at UID 1000, so this could create a UID conflict.

That should do it! In the next video, I'll show how to configure another Ubuntu VM to use this LDAP server for authentication.
