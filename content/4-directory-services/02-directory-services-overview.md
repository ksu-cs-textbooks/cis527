---
title: "Directory Services Overview"
weight: 10
pre: "2. "
---

{{< youtube  >}}

#### Resources

* **[Slides]({{< relref "/4-directory-services/02-directory-services-overview-slides.md" >}})**
* [X.500 Standard](http://www.x500standard.com/)
* [Active Directory](https://en.wikipedia.org/wiki/Active_Directory) on Wikipedia
* [Lightweight Directory Access Protocol (LDAP)](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol) on Wikipedia
* [Samba (Software)](https://en.wikipedia.org/wiki/Samba_(software)) on Wikipedia
* [NetIQ eDirectory](https://en.wikipedia.org/wiki/NetIQ_eDirectory) on Wikipedia (previously Novell Directory Services)
  * [Overview of Novell Directory Services](http://support.novell.com/techcenter/articles/dnd19970304.html) from Novell
* [Kerberos (Protocol)](https://en.wikipedia.org/wiki/Kerberos_(protocol)) on Wikipedia
  * [RFC 1510 - Kerberos](https://tools.ietf.org/html/rfc1510) from IETF
* [Directories, Directory Services, and LDAP](https://directory.apache.org/apacheds/basic-ug/1.2-some-background.html) from Apache
* [Understanding Workgroups and Domains](http://etutorials.org/Microsoft+Products/microsoft+windows+xp+professional+training+kit/Chapter+1+-+Introduction+to+Windows+XP+Professional/Lesson+3nbspUnderstanding+Workgroups+and+Domains/) from eTutorials.org

#### Video Transcript

This video presents a brief overview of directory services and related concepts. This information is very helpful in understanding the larger role that many of these services play in modern computer networks.

At its core, a directory service is simply a piece of software that can store and retrieve information. The information stored could take many forms, including user accounts, groups, system information, resources, security settings, and more. By providing a centralized location to store that information, it becomes much simpler to share that information across a large enterprise network.

We've already worked with one example of a directory service in this course. The modern Domain Name Service is, at its core, a directory service. It stores a directory of domain names matched to IP addresses, as well as additional information about a domain such as the location of the mail server. It can then provide that information to the systems on a large network, providing a level of consistency that is difficult to achieve if each computer has to store a local version of the same information.

Directory services for computers have also been around for quite a while. This page gives a brief timeline of events, starting in the late 1980s and culminating with the release of Microsoft's Active Directory Domain Services in 1999. Let's look at each of these items in detail.

First, the X.500 set of standards was released in 1988, and was one of the first projects that aimed to provide a consistent directory of user account information. It was actually developed as a directory for the X.400 set of standards for email, which at that time was the dominant way that email was handled on the internet. Those standards were developed using the OSI networking protocols. However, with the rise of the TCP/IP set of internet protocols, these systems were quickly made obsolete. X.400 was replaced by the SMTP standards used today to send email between MTAs, while X.500 forms the basis of many later protocols. What is most notable about X.500 is that it actually defined several underlying protocols, including a Directory Access Protocol (DAP), as well as a Directory System Protocol (DSP) and others. Today, we primarily use protocols based on the original DAP defined by X.500.

Soon after the release of the X.500 standards, work began on an implementation of the DAP protocol using the TCP/IP internet protocols. It was eventually named the Lightweight Directory Access Protocol, or LDAP. LDAP is the underlying protocol used by many of todays directory services, including Microsoft Active Directory.

However, it is very important to understand that LDAP is not a complete implementation of the original X.500 DAP. Instead, it implements a core set of features, and then adds some additional features not present in the original protocol, while several parts of the original protocol are not implemented. The maintainers of the X.500 standard are very quick to point out this difference, but in practice most systems fully support LDAP as it stands today.

LDAP also has uses beyond just a directory service for user accounts on workstations. For example, LDAP can be used to provide a user lookup service to an email client, or it can be linked with a website to provide user authentication from a central repository of users.

LDAP, along with many other directory services, defines a tree structure for the data. In this way, the data can be organized in a hierarchical manner, closely resembling the real relationships between people, departments, and organizations in an enterprise. For example, in this diagram, you can clearly see nodes in the tree for the overarching organization, the organizational unit, and the individual user.

LDAP uses several short abbreviations for different fields and types of data, and at times they can be a bit confusing to new system administrators. This slide lists a few of the most common ones, as well as a good way to remember them. For example, an `ou` in LDAP is an organizational unit, which could be a department, office, or some other collection of users and systems.

You can see these abbreviations clearly in this sample LDAP entry. Here, we can see the distinguished name includes the canonical name, as well as the domain components identifying its location in the tree. We can also see the common name and surname for this user, as well as the distinguished name for his supervisor. As you work with LDAP throughout this module, you'll see data presented in this format several times.

Switching gears a bit, in the early 1990s, there were many different software programs developed to help share files and users between systems. One of the first was Samba. Samba is an open source project that originally reverse engineered the SMB (hence the name) and CIFS file sharing protocols used by Windows. By doing so, they were able to enable file sharing between Linux based systems, including Macs, and Windows. Eventually, Microsoft worked with the developers of the project to allow them to fully implement the protocol, and in more recent versions, a computer running Samba can even act as part of an Active Directory domain. We'll work with Samba a bit later this semester when we deal with application servers.

Around the same time, Novell released their Directory Services software. This was one of the first directory services targeted at large organizations, and for many years it was the dominant software in that area. It was built on top of the IPX/SPX internet protocols, so it required computers to run special software in order to use the directory service.

Much like the LDAP example earlier, NDS also supported a tree structure for storing information in the directory. It also had some novel features for assigning permissions across different users and `ou`s, which made it a very powerful tool. Many older system administrators have probably worked with Novell in the past. I remember that both my high school, as well as some departments at K-State, used NDS until they switched to Microsoft Active Directory in the mid 2000s.

Before we discuss Active Directory, we should first discuss Windows Workgroups and Homegroups. Most home networks don't need a full directory service, but it is very helpful to have a way to share files easily between a few computers connected to the same network. Prior to Windows 7, Windows used a "Workgroup" to share these files.

Computers with the same Workgroup name would be able to discover each other across a local network, and any shared files or resources would be available. However, user accounts were not shared, so you wanted to access a resource shared from a particular computer, you'd have to know a username and password for that system as well. For smaller networks, this usually wasn't a problem at all. However, as the network grows larger, it becomes more and more difficult to maintain consistent user accounts across all systems.

That all changed in 1999 with the introduction of Microsoft Active Directory. It coincided with the release of Windows 2000, one of the first major Windows releases directly targeted at large enterprises. Active Directory uses LDAP and Kerberos to handle authentication, and provides not only a central repository of user accounts and systems, but it can also be used to share security configurations across those systems as well. It was really ideal for large enterprise networks, and gave administrators the level of control they desired. Active Directory quickly became the dominant directory service, and most enterprises today use Active Directory to manage user accounts for their Windows systems. In fact, both K-State and K-State Computer Science primarily use Active Directory to manage their user accounts across a variety of systems and platforms.

With a shared domain, the user account information is stored on the central domain controller, instead of the individual workstations. In this way, any user who has a valid account on the domain and permissions to access a resource can do so, regardless of which system they are connected to. This is what allows you to use the same user account to log on to computers across campus, as well as online resources such as webmail and Canvas. One of the major activities in this lab will be to install and configure an Active Directory Domain, so you can get first-hand experience of how this works.

Lastly, no discussion of directory services would be complete without discussing Kerberos. Kerberos is named after Cerberus, the three-headed dog from ancient Greek mythology. It allows a client and a server to mutually authenticate each other's identity through a third party, hence the three-headed mascot.

Kerberos was originally developed at MIT in the 1980s, and fully released in 1993 as RFC 1510. It is one of the primary ways that directory services today handle authentication, and it is used by many other types of security software on the internet today.

The Kerberos protocol is quite complex, and it uses many different cryptographic primitives to ensure the communication is properly secured and authenticated. However, this diagram gives a quick overview of the protocol and how it works.

1. First, the client will communicate with the authentication server.
2. The server responds with two messages, labelled A and B in this diagram. Message A is encrypted by the server using the client's key. When the client receives that message, it attempts to decrypt it. If it is successful, it can use the contents inside the message to prove its identity.
3. Then, it can send two new messages, C and D, to the ticket granting server, which in practice is usually the authentication server, but it doesn't have to be. Message C includes the contents of message B along with information about what the client would like to access, and message D is the decrypted contents of the original message A. The ticket granting server then looks at those messages and confirms the user's identity.
4. If it is correct, it will then send two more messages, E and F, to the client. Message E is the ticket that can be given to the server containing the desired resource, and message F contains a key that can be used to communicate with that server.
5. So, the client finally can contact the destination server, sending along message E, the ticket from earlier, as well as a new message G that is protected with the key contained in message F.
6. Finally, the server decrypts message G and uses it to create and send back message H, which can be confirmed by the client to make sure the server is using the same key.

If everything works correctly, both the client and server know they can trust each other, and they have established keys that allow them to communicate privately and share the requested information. Kerberos is a very powerful protocol, and if you'd like to learn more, I highly recommend reading the linked resources below this video. Kerberos is also discussed in several of the cybersecurity courses here at K-State.

That's all the background information you'll need for this module. Next, you'll work on installing Microsoft Active Directory on Windows and OpenLDAP on Ubuntu, as well as configuring clients to use those systems for authentication. 
