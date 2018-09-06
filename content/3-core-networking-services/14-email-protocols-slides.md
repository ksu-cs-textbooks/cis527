---
type: "reveal"
hidden: true
---
<section>
	<h2>CIS 527</h2><br><br><p>Lab 3 - Email Protocols</p>
</section>
<section>
	<h3>Electronic Mail (email)</h3>
	<ul>
		<li>Send Messages Across the Internet</li>
		<li>Developed in 1970s as Extension to FTP</li>
		<li>Originally Text Only</li>
		<li>Extended by Multipurpose Internet Mail Extensions (MIME)</li>
	</ul>
</section>
<section>
	<h3>Email Protocols</h3>
	<ul>
		<li>Simple Mail Transfer Protocol (SMTP)</li>
		<li>Post Office Protocol (POP3)</li>
		<li>Internet Message Access Protocol (IMAP)</li>
		<li>Exchange ActiveSync</li>
	</ul>
</section>
<section>
	<h3>Email Server Components</h3>
	<ul>
		<li>Mail Transfer Agent (MTA)</li>
		<li>Mail Delivery Agent (MDA)</li>
		<li>IMAP/POP/Webmail Server</li>
	</ul>
</section>
<section>
	<img class="stretch plain" src="/images/email_wiki.svg">
	<p class="imagecredit">Image Source: <a href="https://en.wikipedia.org/wiki/Email">Wikipedia</a></p>
</section>
<section>
<pre style="font-size: .4em"><code>cis527@cis527russfeldpuppet:~$ telnet mail.servergrove.com 110
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
+OK Bye-bye.</code></pre>
</section>
