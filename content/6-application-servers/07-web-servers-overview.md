---
title: "Web Servers Overview"
weight: 35
pre: "7. "
---

{{< youtube  >}}

#### Resources

* **[Slides]({{< relref "/6-application-servers/07-web-servers-overview-slides.md" >}})**
* [Web Server](https://en.wikipedia.org/wiki/Web_server) on Wikipedia
* [LAMP (Software Bundle)](https://en.wikipedia.org/wiki/LAMP_(software_bundle)) from Wikipedia
* [Nginx](https://en.wikipedia.org/wiki/Nginx) from Wikipedia
* [Web Server Survey](https://news.netcraft.com/archives/category/web-server-survey/) from Netcraft

#### Video Transcript

Another common type of application server in many enterprises is a web server. A web server is the software that is used to make websites available on the World Wide Web. So, it is responsible for listening and responding to HTTP requests. The software is typically designed so it can handle many simultaneous connections, and even serve multiple websites as we saw in Lab 5. Additionally, many web servers support features for caching and server-side scripting languages, making them a truly versatile platform for serving both web pages and web-based applications.

There are a three web servers that are currently the most commonly used on the internet today. We'll be looking at two of them in this module. The first is Apache. It was one of the earliest web servers, and because it was free and open source, it drove much of the early expansion of the web in the 1990s and 2000s. While Apache is technically available for a number of different platforms, it is most commonly found running on Linux systems. As of September 2018, it runs 23% of all websites on the internet, and 34% of all domain names use Apache, according to Netcraft. While it has been declining in market share over the past several years, Apache is still one of the most commonly used web servers on the internet today.

On many systems, Apache is typically part of the larger LAMP software stack. LAMP typically stands for "Linux, Apache, MySQL, PHP" but other databases and scripting languages also fit the initialism. As part of this lab's assignment, you'll install a LAMP stack and a web application running on that platform.

The next web server we should discuss is Nginx (pronounced "engine-x"). Nginx was developed as a successor to Apache, with a focus on high throughput and the ability to handle a large number of simultaneous connections. According to the documentation, it is able to handle 10,000 inactive connections on just 2.5 MB of RAM. While Nginx doesn't support as many scripting languages and plugins as Apache, it's high performance makes it a very popular choice for websites expecting a large amount of traffic. As of September 2018, Nginx powered 19% of websites and 23% of all domains on the internet, and it has been slowly climbing the ranks since its release.

The last web server we'll work with during this lab assignment is Microsoft's Internet Information Services, or IIS. IIS is included in all versions of Windows, though typically it is not installed by default on the consumer versions of the operating system. Like Apache, IIS is able to support web applications written in the .NET family of languages. As of September 2018, IIS powers 36% of websites on the internet, making it the most popular web server in that regard. However, it is only present on 26% of domains, putting it behind Apache in that metric.

As mentioned earlier, both Apache and IIS, as well as Nginx through the use of some additional software, are able to support a large range of scripting languages to power interactive web applications. Some of the more commonly used languages are listed here, from PHP and Python to the .NET family of languages, and even Java and JavaScript. As you work on this lab assignment, you'll get to learn a bit about how to work with web applications written in a couple of these languages.

The next few videos will cover the steps needed to complete the rest of this lab assignment. First, you'll need to make sure the web server is installed and configured properly. You'll also have to configure the domain name for the website, and handle installing a security certificate. Finally, you'll be able to install an application that uses one of the scripting languages supported by the server, and see how it all works together to present a web application to your users.
