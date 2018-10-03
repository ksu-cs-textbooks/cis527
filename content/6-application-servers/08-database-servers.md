---
title: "Database Servers"
weight: 40
pre: "8. "
---

{{< youtube  >}}

#### Resources

* **[Slides]({{< relref "/6-application-servers/08-database-servers-slides.md" >}})**
* [5 Tips for Managing Database Servers in Production](https://blog.cloud66.com/5-tips-for-managing-database-servers-in-production/) from Cloud 66
* [10 Essential Performance Tips for MySQL](https://www.infoworld.com/article/3210905/sql/10-essential-performance-tips-for-mysql.html) by Baron Schwartz on InfoWorld
* [10 Easy Tips for Better SQL Server Performance](https://www.itprotoday.com/sql-server/10-easy-tips-better-sql-server-performance) from ITPro Today
* [What Kind of Disks Should You Use with Microsoft SQL Server 2016?](https://blog.heroix.com/blog/what-kind-of-disks-should-you-use-with-microsoft-sql-server-2016-part-1) from Heroix Blog
* [Database Encryption](https://en.wikipedia.org/wiki/Database_encryption) on Wikipedia
* [Encrypting Data at Rest on Servers: What Does it Get You?](https://hln.com/encrypting-data-at-rest-on-servers-what-does-it-get-you/) from HLN Consulting

#### Video Transcript

One of the other most commonly used application servers in an enterprise is a database server. You may also see the term "Database Management System" or "DBMS" used in some areas to refer to the same thing. A database server is typically the backbone of your organization's data storage, as it can be used to store and retrieve a large amount of data very efficiently. Depending on the server software, the data may be stored in large files on the file system, or the database server may work directly with a block-level storage device for even more performance.

Of course, since a database server is constantly reading and writing data, it has some very unique performance and storage needs. We'll discuss a few of those at the end of this video. In addition, as a system administrator, you'll definitely be tasked with creating backups, and you may also handle replication across multiple database servers. We'll spend a bit of time discussing backups in Module 7.

Unfortunately, working with database servers can be one of the most complex tasks a system administrator handles, and, in fact, many organizations use a different title, "database administrator" or "DBA," to refer to staff who are primarily responsible for working with database servers. Because it is such a complex topic, we really won't be spending much time working directly with database servers other than performing basic setup and configuration. If you are interested in working with a particular database server, I encourage you to read some of the information in the resources section below the video to learn more about this topic.

There are a few different database systems that are commonly used in industry today. Unlike web servers, where the vast majority of organizations use one of just three systems, there are many more database servers widely in use today. I'll briefly talk about a few of the most common that you'll come across today.

First is MySQL, and its fork, MariaDB. MySQL was originally developed in the late 1990s as an open source project, freely licensed under the GPL. As with Apache, it gained widespread use and acceptance among Linux enthusiasts, and was a commonly used database in many open source projects such as WordPress and Drupal, as well as major websites such as Flickr, YouTube, and Twitter. In 2010, MySQL was acquired by Oracle, and while it still retains its open source status at this time, many developers feared that Oracle may eventually move the software to a proprietary license. So, MariaDB was created as a fork of MySQL to maintain a public license. MariaDB maintains full compatibility with MySQL, and the two systems can be used pretty much interchangeably in practice. As part of this lab assignment, you'll install and work with MySQL in the cloud.

Another commonly used database system is Postgres. Postgres is very similar to MySQL in terms of licensing and features, but it aims to be as "standards compliant" as possible. Because of this, many professionals prefer Postgres due to the fact that it meets some of the standards that MySQL does not.

Microsoft also has their own database server, named Microsoft SQL Server. This is typically used along with the .NET family of programming languages on Windows systems. While we won't work directly with Microsoft SQL Server, as part of the lab assignment you'll install a .NET web application which most likely uses a local database that is similar to Microsoft SQL Server.

Oracle, of course, is another major database system in use today. They are well known for providing enterprise-level database software, and have been doing so since the 1970s. Because of this, many older organizations have been using Oracle's database software for some time, including K-State. Most of K-State's central systems, including KSIS and HRIS, are built on top of Oracle database products.

Lastly, there are a number of new database systems that include features such as document or object storage and "NoSQL" schemas. One of the most popular of those is MongoDB. These systems are most commonly used with web applications and some big data analytics packages.

As I mentioned earlier, working with a database server presents some very interesting and unique performance considerations that you may have to deal with as a system administrator. First, you'll definitely be concerned with the amount of RAM that the system has available. Ideally, you'd like to have plenty of RAM available for the system so that it can hold a large amount of data and indexes directly in memory, making requests as fast as possible. You'll also want to prevent paging of data if at all possible. If the server is unable to store everything it needs directly in RAM, it can make your server up to 50 times slower as it handles paging.

Your CPU speed is also a factor, as that impacts how quickly the system can perform indexing and querying of the data, especially if many complex queries are needed. In addition, another major concern is the read and write speeds of the filesystem. You may want to consider using high performance SSDs in your database server, coupled with a RAID configuration using RAID 1+0 or RAID 6 to gain additional performance and data security. There is a great discussion of these storage considerations linked in the resources section below the video.

Beyond the hardware, you may also have to deal with issues such as the network speed and throughput to your database server. In some cases, you may even need to install multiple network interfaces for a database system if you find that the network interface is constantly saturated but the database server itself is not running near capacity. Also, many database servers maintain a separate log file from the data, which is used to verify that data updates are made properly. For large systems, it is generally recommended to store that log file in a separate location, so that updates to both the data and the log file can be done in parallel. Finally, as with any system, you'll want to set up plenty of monitoring and alerts on your database server, so you can quickly respond to problems as they arise. We'll discuss a bit of information about monitoring in Module 7.

You'll also need to spend some time thinking about the security of your database server. Just like with any other system, you'll want to make sure any network connections to and from this server are properly secured. Most database servers support using TLS to secure the connection between a database server and the application using it, but in many cases it must be configured and is not enabled by default. In general, it is also recommended to prevent external access to your database server. This is generally done through a firewall that only allows incoming connections from the application servers or a select number of internal IP addresses.

Another major concern with database servers is encryption. Depending on the type of data you are working with, there may be two different levels of encryption to consider. First, you should consider encrypting the data when it is at rest, or stored on the disk itself. Typically this is handled through full-disk encryption, file system encryption, or even encryption of the database tables themselves through the database server software. Each option comes with tradeoffs in terms of performance and security, so you should carefully research the options to determine the best choice for your environment.

Encrypting the data at rest, unfortunately, does not protect the data if a malicious user manages to gain access to the database system itself while it is running. So, you may also want to encrypt data stored in the tables themselves so that it is only readable by the application using the data. Some examples of data you may want to encrypt are usernames, email addresses, phone numbers, and any other personal information for your users. The details of how to do this properly are definitely outside the scope of this course, but there are many great resources online and elsewhere to learn how to secure data stored in an application.

Lastly, as a system administrator, you may want to keep an eye out for data being copied from your database server in an unexpected way. Typically, when a malicious user gains access to a database server, the first thing she or he will do is try to get a copy of that data on their own systems. This is called "exfiltration," and is a major concern for enterprises. As part of your security and monitoring of your database server, you may want to watch for unexpected network connections leading outside of your organization, especially if they are coupled with an unusually large amount of network traffic. It could be a sign that someone is trying to get a copy of your databases.

As I mentioned earlier, this is just a brief introduction to working with database servers. You'll get a bit of experience with MySQL in this lab assignment, but if you are interested in learning more, I encourage you to take courses in database systems and seek additional resources online. Database administrators are always in demand, and it is a great career path to pursue. 
