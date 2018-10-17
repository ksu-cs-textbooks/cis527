---
title: "Ubuntu Web Server"
weight: 55
pre: "11. "
---

{{< youtube  >}}

#### Resources

* [Install MySQL on Ubuntu 18.04 Bionic Beaver Linux](https://linuxconfig.org/install-mysql-on-ubuntu-18-04-bionic-beaver-linux) from LinuxConfig.org
* [How To Configure SSL/TLS for MySQL on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-configure-ssl-tls-for-mysql-on-ubuntu-16-04) from DigitalOcean (works for 18.04)
* [How To Install and Secure phpMyAdmin on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-18-04) from DigitalOcean
* [How To Install the Apache Web Server on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-18-04) from DigitalOcean
* [How To Secure Apache with Let's Encrypt on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-18-04) from DigitalOcean

#### Video Transcript

In this video, I'm going to discuss some of the steps needed to prepare your Ubuntu servers running in the cloud to act as web application servers. For this example, I'll be using a single server as both my web and database server, but for the lab assignment you'll need to adapt this configuration to have the web application installed on your **FRONTEND** server access the database server on your **BACKEND** server.

At this point, you should already have Apache installed, as well as a couple of sites and virtual hosts created from Lab 5. I'm going to use one of those existing virtual hosts as the basis for this web application. Remember that, for the lab assignment, you'll be creating another new virtual host for this application.

First, you'll need to install PHP and it's associated Apache module on your **FRONTEND** server:

```bash
sudo apt update
sudo apt install php libapache2-mod-php
```

That will install and configure PHP on your system. To test it, you can create a new file in the web directory of one of your virtual hosts named `test.php` and add the following content:

```html
<?php phpinfo(); ?>
```

Then, navigate to that virtual host and load the `test.php` file from that website. For my example, I would go to `http://foo.russfeld.me/test.php`. Hopefully you should see a website showing all of the PHP configuration information for your system. Once you confirm it is working, it is always a best practice to delete this `test.php` test file, as the information it provides could be used by a malicious person to attack your server.

Now that we've confirmed that PHP is working, it is time to install the MySQL database server. This time, on your **BACKEND** server, do the following:

```bash
sudo apt update
sudo apt install mysql-server
```

That will install the MySQL server on your system. However, by default it is configured very insecurely, so you'll need to reconfigure it to be more secure. Thankfully, there is a script to do just that:

```bash
sudo mysql_secure_installation
```

That script will ask you a series of questions to help you secure your MySQL server. In general, you should answer "Yes" to all of the questions, and set the password policy to at least "MEDIUM" security. In addition, you'll be asked to set a password for the `root` account on the server. As before, make sure it is very memorable password, and do not reuse any of the passwords we've previously used in this course.

Once that is finished, you can test the connection to MySQL using the following command:

```bash
sudo mysql -u root
```

It should take you to a new prompt that begins with `mysql>`. Once there, we should create a new user for us to use for development. So, enter these commands at that prompt:

```mysql
CREATE USER 'admin'@'localhost' IDENTIFIED BY '<password>';
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' WITH GRANT OPTION;
```

where `<password>` is the password you'd like to use for that account. Once that is done, you can enter:

```mysql
exit
```

to close that connection. Now, you can test the new connection without using `sudo` as follows:

```bash
mysql -u admin -p -h 127.0.0.1
```

It should ask you for a password, and once you enter the password you created for the `admin` account above, it should take you back to the `mysql>` prompt. While there, enter the following command:

```mysql
\s
```

to see the connection information. You'll notice that TLS (SSL) is not enabled. To enable that, follow the steps in the guide from DigitalOcean linked in the resources section below this video. I won't walk through those steps here since you'll doing that as part of your lab assignment. In addition, you'll want to follow the steps in that guide for configuring access for remote clients, as we'll be doing that to configure a web application in the next video.

That should cover everything you need to prepare your system for a web application that uses PHP and MySQL. In the next video, we'll go through the process of installing a simple application in this environment.
