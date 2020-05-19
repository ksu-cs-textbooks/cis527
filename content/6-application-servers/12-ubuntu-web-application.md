---
title: "Ubuntu Web Application"
weight: 60
pre: "12. "
---

{{< youtube G1iN-Aoj0Ow >}}

#### Resources

* [phpBB](https://www.phpbb.com/)
* [Installation](https://www.phpbb.com/support/docs/en/3.2/ug/quickstart/installation/) from phpBB
* [How To Set Up A Remote Database to Optimize Site Performance with MySQL on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-remote-database-to-optimize-site-performance-with-mysql-on-ubuntu-18-04) from DigitalOcean (works for 20.04)

#### Video Transcript

In this video, I'll discuss the steps you'll need to follow in order to install a new web application that uses PHP and MySQL on the environment we created in the last video. As with the previous videos discussing web applications on a Windows server, you'll have to adapt these steps to match the application you are installing and the particular configuration of your environment.

First, we'll need to create a new database and user for this application on our database server. So, first you'll need to log on to the MySQL server using one of the methods we discussed in the previous video to get to a `mysql>` prompt. I recommend using either the `root` or `admin` user for this step, as they both should have the permissions needed to add another user and database.

Once you are at the `mysql` prompt, you can create a database and user for your application:

```mysql
CREATE DATABASE <database>
CREATE USER '<user>'@'<ip_address>' IDENTIFIED BY '<password>';
GRANT ALL PRIVILEGES ON <database>.* TO '<user>'@'<ip_address>';
FLUSH PRIVILEGES;
```

This command is a bit complex, so let's walk through it. In the first line, you'll create a database, replacing `<database>` with the name you'd like to use for that database. In general, it is a good idea to use the name of your application for the database name. On the second line, you are creating a user to access that database, so replace `<user>` with the username you'd like. Again, I recommend using the application name here as well. The `<ip_address>` entry should be the IP address that the user will be accessing this database from. For the lab assignment, you'll be using the private network IP address of **FRONTEND** here. Since I'm working on a single server, I'll just use `localhost` here. Of course, replace `<password>` with the password you'd like to use. The following line grants that user all privileges on that database, so replace the entries on that line to match what you used above. Finally, the last line will flush the permissions cache, so the new ones will take effect. Once you are done, you can type `exit` to exit the MySQL console.

If you'd like to test this connection, on your **FRONTEND** server, you can use the `mysql` command in a similar way:

```bash
mysql -u <user> -p -h <ip_address> <database>
```

In this command, the `<ip_address>` is the private network IP address of your **BACKEND** server. If it works correctly, it should allow you to log in to the MySQL console using that command. If this doesn't work, you should diagnose the problems with your MySQL configuration before continuing.

Now that we have our database configured, it's time to install our application. For this example, I'm going to use phpBB, a bulletin board software built in PHP. It is a very simple example of a PHP web application. First, I'll need to download the software onto my cloud server. The simplest way to do this is to navigate to the Downloads page on the phpBB website and copy the download URL. Then, in my SSH session connected to my server, I can type the following commands:

```bash
cd ~
wget <url>
```

where `<url>` is the download URL I copied from the phpBB site. I made sure I was at my user's home folder first, so I knew where the file would be downloaded to. Next, I'll need to install the `unzip` program, and use it to extract the downloaded file:

```bash
sudo apt update
sudo apt install unzip
unzip <file>
```

where `<file>` is the name of the file that was just downloaded. On my system, it extracted all of its files to the `~\phpBB3` directory.

At this point, we should begin following the instructions for installing and configuring phpBB from their website. I'll generally follow their recommended steps, so feel free to refer to their documentation as well if you are following along.

Now, we need to copy all of those files to the appropriate virtual host root directory. Since I'm reusing an existing virtual host, I'll need to make sure that it is empty before I do so. Remember that the lab assignment directs you to create a new virtual host for this application, so you won't have to worry about that. For my example, I'm going to use the `foo` virtual host:

```bash
sudo rm -rv /var/www/foo/html/
sudo cp -r ~/phpBB3/* /var/www/foo/html/
```

Next, while the instructions don't have you do this, I'm going to change the ownership of all of these files to the Apache user, which is `www-data`. This will make assigning permissions in the next step a bit simpler:

```bash
sudo chown -R www-data:www-data /var/www/foo/html
```

Next, the instructions direct you to access your site's URL via a web browser. So, I'll need to navigate to `http://foo.russfeld.me` to continue this process.

On the first page of the installation process, it will check to see if the server meets the necessary requirements for this software. Unfortunately, that isn't the case yet. If you receive any error messages about directories that aren't writable, you may need to adjust your permissions for those directories. By setting the owner and group to `www-data` earlier, I have bypassed most of those errors.

However, it complains that I don't have XML/DOM support, and I don't have a PHP database module installed. So, I'll need to install those items. A quick Google search should help you locate them if you aren't sure what packages you need to install. In my case, I'll do the following:

```bash
sudo apt update
sudo apt install php-xml php-mysql
sudo systemctl restart apache2
```

{{% notice warning %}}
_Update 2019-07-30: You may need to install the version of `php-mysql` that matches your PHP version. So, for PHP 7.2, you can install `php7.2-mysql`. -Russ_
{{% /notice %}}

Once that is done, I should be able to retest the requirements and get to the next step. Here, it will ask for the information to create an Administrator account. I'll enter some default information here.

Next, you'll need to configure the database for this system. I'll enter the information for the database and user I created earlier. I'll also enter the IP address `127.0.0.1` for my server hostname. For the lab assignment, you'll need to use the private network IP address of **BACKEND** here. On the next screens, I'll configure some additional options unique to phpBB, selecting the appropriate options for my environment and how I'd like to use the application. Finally, it will go through the installation procedure. If everything works properly, it should be able to connect to your database and install the application.

Now, I can go to the control panel for phpBB and create a new forum, just to make sure that it is working properly.

Finally, you may have to do additional configuration to set up your Virtual Host to use a security certificate and redirect to HTTPS using Certbot, if you haven't already.

There you go! You've now successfully installed and configured a web application using PHP on Apache, and connected it to a MySQL database running on a different system. In addition, everything is properly secured using TLS, firewalls, and other state-of-the-art security settings. Feels pretty good, doesn't it?

That should give you everything you need to complete this lab assignment. This lab is quite a bit more open-ended than previous assignments, since you'll have the ability to work with a web application of your choice. If you have any questions or run into any issues getting this lab assignment completed, please post in the course discussion forums as always to get help. Good luck!
