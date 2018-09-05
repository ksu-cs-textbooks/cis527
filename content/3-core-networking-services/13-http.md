---
title: "HTTP"
weight: 65
pre: "13. "
---

{{< youtube  >}}

#### Resources

* **[Slides]({{< relref "/3-core-networking-services/13-http-slides.md" >}})**
* [Hypertext Transfer Protocol (HTTP)](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol) on Wikipedia

#### Video Transcript

Next, let's review a couple of application layer protocols. One of the most common of those is the Hypertext Transfer Protocol, or HTTP.

HTTP was developed by Tim Berners-Lee while he worked at CERN in the late 1980s as part of his project to build the World Wide Web. HTTP itself is an application-layer protocol that is built on top of the TCP transport-layer protocol. As with many early application-layer protocols, it is actually a text-based protocol, making it very easy to read and work with manually if desired. HTTP is the protocol used to access webpages on the World Wide Web. In fact, if you look at the address bar of most web browsers, you'll still see `http://` in front of web addresses, indicating that it is using the HTTP protocol to access that site.

Since HTTP is a text-based protocol, it defines a set of commands and responses to make it easy for the system to understand each packet. The two most common HTTP commands are `GET` and `POST`. `GET` is used to request a webpage from a server, and `POST` is used to submit information back to the server, usually as part of a form on the website. Other commands are defined, but they are generally not used very often.

When the server responds to a command from a client, it sends along a numerical status code for the response. Some of the common status codes are listed here. For example, `200` means that the request was accepted properly, whereas `404` indicates that the requested resource was not fond on the server. You've probably seen some of these error codes in your web browser from time to time.

As I mentioned earlier, HTTP is a text-based protocol. That means, if you are able to type quickly enough, you can use a text-based program such as Telnet to actually send queries directly to a web server. This image shows an HTTP request and response sent using Telnet to the main Wikipedia server.

Let's see if we can recreate this connection on our own system. Once again, I'm going to use my Ubuntu server configured as directed for Lab 3. I'm also going to start Wireshark so we can capture these packets. I'll add a filter for `http` to make sure we only see the HTTP packets.

To initiate an HTTP connection, we'll use the `telnet` command to connect to a server on port 80:

```bash
telnet cs.ksu.edu 80
```

That should connect you to the server. Once connected, you can request the homepage using this HTTP command:

```http
GET /index.html HTTP/1.0
Host: cs.ksu.edu

```

Once you leave a blank line, the server should respond. In this case, you should get the following headers in your response:

```http
HTTP/1.1 301 Moved Permanently
Date: Wed, 05 Sep 2018 19:47:12 GMT
Server: Apache/2.4.25 (Debian)
Location: http://www.cs.ksu.edu/index.html
Content-Length: 316
Connection: close
Content-Type: text/html; charset=iso-8859-1
```

Looking at the response, you can see that the status code is `301 Moved Permanently`, letting me know that the page is available at a different location. A little bit later, it gives the new location as `http://www.cs.ksu.edu/index.html`. So, I'll have to query that server instead.

```bash
telnet www.cs.ksu.edu 80
```

```http
GET /index.html HTTP/1.0
Host: www.cs.ksu.edu

```

Once I do that, I should now get a proper web page as the response:

```http
HTTP/1.1 200 OK
Date: Wed, 05 Sep 2018 19:49:59 GMT
Server: Apache/2.4.25 (Debian)
Accept-Ranges: bytes
Vary: Accept-Encoding
Connection: close
Content-Type: text/html

<!DOCTYPE html>
<html lang="en-US"><head>
...
```

Going back to Wireshark, we should clearly see those HTTP packets. You can see each request packet, followed by the response including the status code. If you examine the contents of the packets, you'll see that it exactly matches what we were able to receive using `telnet`. It's really that simple.

Now, let's do one more quick example, just to see one of the weaknesses of the HTTP protocol. Some early websites required authentication using the HTTP protocol. However, unless you use a security layer such as TLS, those packets would not be encrypted whatsoever, and anyone able to capture the packet could decode the username and password. Let's see what HTTP authentication would look like using `telnet`.

First, we'll have to create a base64 encoding of our username and password. These are the same credentials used in the lab assignment:

```bash
echo -n cis527:cis527_apache | base64 -
```

The output should be `Y2lzNTI3OmNpczUyN19hcGFjaGU=`, which is what we'll use for the next command.

Now, let's use `telnet` to connect to our secured page:

```bash
telnet people.cs.ksu.edu 80
```

```http
GET /~russfeld/test/ HTTP/1.0
Host: people.cs.ksu.edu
Authorization: Basic Y2lzNTI3OmNpczUyN19hcGFjaGU=

```

If it works correctly, you should receive a response like the following:

```http
HTTP/1.1 200 OK
Date: Wed, 05 Sep 2018 20:06:10 GMT
Server: Apache/2.4.10 (Debian)
Last-Modified: Wed, 17 Feb 2016 16:48:27 GMT
ETag: "5e-52bfa04e3af09"
Accept-Ranges: bytes
Content-Length: 94
Vary: Accept-Encoding
Connection: close
Content-Type: text/html

<html>
<head>
	<title>Congrats!</title>
</head>
<body>
Congrats! You did it!
</body>
</html>
```

So, even though it looks like the username and password are encrypted, they are easily deciphered using any base64 decoding program. As part of the lab assignment, you'll capture an authentication packet just like this one in Wireshark.

This is just a quick introduction to HTTP. There are many interesting features in the protocol, and they are easy to explore by simply capturing packets with Wireshark while you use a web browser to surf the World Wide Web. I encourage you to do just that to get a bit more experience with HTTP.
