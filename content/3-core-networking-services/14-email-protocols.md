---
title: "Email Protocols"
weight: 70
pre: "14. "
---

{{< youtube lcg43SAJv5Q >}}

#### Resources

* **[Slides]({{< relref "/3-core-networking-services/14-email-protocols-slides.md" >}})**
* [Email](https://en.wikipedia.org/wiki/Email) on Wikipedia
* [Simple Mail Transfer Protocol (SMTP)](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol) on Wikipedia
* [Post Office Protocol (POP3)](https://en.wikipedia.org/wiki/Post_Office_Protocol) on Wikipedia
* [Internet Message Access Protocol (IMAP)](https://en.wikipedia.org/wiki/Internet_Message_Access_Protocol) on Wikipedia
* [Why You May Not Want to Run Your Own Mail Server](https://www.digitalocean.com/community/tutorials/why-you-may-not-want-to-run-your-own-mail-server) from DigitalOcean

#### Video Transcript

In this video, we'll look at one more set of application layer protocols, the ones for sending and receiving electronic mail, or email.

Email was developed in the early days of the ARPANET, and was originally built as an extension to the existing File Transfer Protocol or FTP. Using these email protocols, a user on one system could send a message to a user on another system. Email was originally designed to be a text-only format, but the later introduction of the Multipurpose Internet Mail Extensions, or MIME, allowed emails to include additional content such as HTML markup, images, and more.

To send and receive email across the internet, there are a number of protocols involved. First, the Simple Mail Transfer Protocol (SMTP) is used to send mail from an email client to a server, and then between the servers until it reaches its desired recipient. Once there, the recipient can use either the Post Office Protocol (POP3), the Internet Message Access Protocol (IMAP), Microsoft's Exchange ActiveSync, or any number of webmail clients to actually view the email.

On an email server itself, there are several pieces of software involved in sending and receiving email. First, the Mail Transfer Agent (MTA) is responsible for SMTP connections, and is primarily used to send and receive email from other email servers. Next, the Mail Delivery Agent (MDA) will receive email from the MTA destined for users on this server, and will route it to the appropriate mailbox. Finally, there are any number of ways to get the email from the mailbox to the user, using the POP3, IMAP, or any number of other protocols. Or, as is often the case today, the user can simply view the email in a web browser, using a webmail client.

To see how email is routed through the internet, here is a nice diagram from Wikipedia showing the process. When Alice wants to send an email to Bob, she must first compose the email and send it to her local MTA using the SMTP protocol. Then, the MTA will use a DNS lookup to find the MX entry for Bob's email domain, which is `b.org` in this example. Then, the MTA can send that email to Bob's MTA, which will then pass it along to the MDA on that system, placing it in Bob's mailbox. Finally, Bob can then use a protocol such as POP3 to read the email from his mailbox onto his computer.

As with many other application layer protocols, several of the core email protocols are text-based as well, and can easily be done by hand using `telnet`. This slide shows what it would look like to use `telnet` to receive email using the POP3 protocol. However, most email servers today require the use of a secure protocol when accessing an email account, so it is difficult to perform this activity today.

```bash
cis527@cis527russfeldpuppet:~$ telnet mail.servergrove.com 110
Trying 69.195.222.232...
Connected to mail.servergrove.com.
Escape character is '^]'.
+OK POP3 ready
USER test@beattieunioncemetery.org
+OK
PASS uns3cur3
+OK logged in.
STAT
+OK 2 5580
RETR 1
+OK 4363 octets follow.
Received: (qmail 11929 invoked from network); 26 Feb 2016 16:16:14 +0000
Received-SPF: none (no valid SPF record)
Received: from mx-mia-1.servergrove.com (69.195.198.246)
  by sg111.servergrove.com with SMTP; 26 Feb 2016 16:15:43 +0000
...
...
...
DELE 2
+OK message 2 deleted
QUIT
+OK Bye-bye.
```

However, many SMTP servers still support sending email via an unsecured connection. This is mainly because there are several older devices such as printers, copiers, network devices, and security devices that are all designed to send alerts via email. Those older devices are difficult if not impossible to upgrade, so many system administrators are forced to use an unsecured SMTP server to accept those notification emails. So, we can use one of those to perform this quick test and see how it works.

For this example, I will connect to the K-State CS Linux servers, as the server we are using will only accept emails from a limited number of systems, including these servers. In addition, it will only accept email sent to a limited number of domains. Both of these protections are in place to limit the amount of unsolicited SPAM email that could be sent using this server.

First, I'll use `telnet` to connect to the email server on port 25, the well-known port for SMTP:

```bash
telnet smtp.cs.ksu.edu 25
```

Then, I'll need to establish a connection with it, send my email, and close the connection. To make it easier to see below, I've prefixed the messages from the server and my telnet client with `###`:

```bash
### Trying 129.130.10.29...
### Connected to daytona.cs.ksu.edu.
### Escape character is '^]'.
### 220 daytona.cis.ksu.edu ESMTP Postfix (Debian/GNU)
HELO daytona.cs.ksu.edu
### 250 daytona.cis.ksu.edu
MAIL FROM: testuser@ksu.edu
### 250 2.1.0 Ok
RCPT TO: russfeld@ksu.edu
### 250 2.1.5 Ok
DATA
### 354 End data with <CR><LF>.<CR><LF>
From: "Russell Feldhausen"
To: "Test"
Date: Fri, 6 September 2018 10:00:00 -0700
Subject: Test Message

This is a test! Hope it Works!

.
### 250 2.0.0 Ok: queued as 827D23FDD1
QUIT
### 221 2.0.0 Bye
### Connection closed by foreign host.
```

Once I have completed that process, I should receive the email in my inbox shortly. You'll notice that there are many things interesting about this email. First, my email client reports the correct date and time that it was received, but at the top of the email itself it gives a different timestamp for when it was sent. Additionally, even though I used my own email address as the recipient, in the email header I listed the name "Test" as the recipient, which is what appears in the email client.

I hope that this example clearly demonstrates how easy it is to spoof any part of an email. The email servers and protocols themselves don't enforce many rules at all, so it is easy to abuse the system, leading to the large amount of SPAM email we receive on a daily basis. However, I still find it fascinating to see behind the curtains a little at how these protocols are actually structured and how easy it is to work with them.
