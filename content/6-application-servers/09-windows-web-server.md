---
title: "Windows Web Server"
weight: 45
pre: "9. "
---

{{< youtube iJr9Q_cR_lg >}}

#### Resources

* **[URL Rewrite](https://www.iis.net/downloads/microsoft/url-rewrite) from Microsoft**
* [Add A Website to Windows Server 2016 using Host Headers](https://www.ionos.com/community/server-cloud-infrastructure/windows-server/add-a-website-to-windows-server-2016-using-host-headers/) from Ionos by 1&1
* [How to Create a Self Signed Certificate in IIS](https://aboutssl.org/how-to-create-a-self-signed-certificate-in-iis/) from AboutSSL
* [Microsoft Server 2016 - IIS 10 & 10.5 - SSL Installation](https://www.sslsupportdesk.com/microsoft-server-2016-iis-10-10-5-ssl-installation/) from SSLSupportDesk
* [How to Install a SSL Certificate on IIS 10](https://helpdesk.ssls.com/hc/en-us/articles/115000853911-How-to-install-a-SSL-certificate-on-IIS-10) from SSLs.com
* [Setting up an HTTP/HTTPS Redirect in IIS](https://www.namecheap.com/support/knowledgebase/article.aspx/9953/38/setting-up-an-httphttps-redirect-in-iis) from Namecheap

#### Video Transcript

In this video, I'll discuss some of the steps for installing and configuring the Internet Information Services, or IIS, web server on Windows Server 2016. This will set the stage for the next video, which will discuss the process for installing a .NET-based web application.

As before, I'll continue to use my Windows Server 2016 VM from previous labs. To install IIS, click on the **Manage** button in the Server Manager application, and select **Add Roles and Features**. From there, you'll follow the same steps you did when you installed the Active Directory Domain Services role, but this time choose the "Web Server (IIS)" role instead. Then, click **Next** a couple of times until you reach the **Select Role Services** page. There, you'll need to checkmark the option for "HTTP Redirection," which can be found under the "Web Server > Common HTTP Features" list items. Also, enable the option for "ASP.NET 4.6" found under the "Web Server > Application Development" list items. When you do so, it may enable a few additional options. Finally, click **Next** once again, then click **Install** to install the new server role.

Once it has been installed, you should now see the new **IIS** option on the left side of the Server Manager application. Click that option to see information about your IIS server. To access the configuration options for that server, let's open the **Internet Information Services (IIS) Manager**, which can be found on the Tools menu in Server Manager, or by right-clicking the entry here.

IIS Manager provides a convenient way to manage and configure your IIS server. Starting on the home page, you'll see icons for a variety of features that you may want to configure for your server. For this video, I'm going to go through the process of adding a new website to this server, as well as the steps to properly configure and secure it.

First, let's create the directory for our new site. I'm going to create a new folder at `C:\inetpub\example` to store the website. The `C:\inetpub` folder on Windows is the default location for IIS to place files, so it is a good logical place for this to be stored. Then, inside of that folder, I can place a simple file named `index.html` to act as the homepage for this website. I'll add a bit of text to the file as well, just so it is clear that we are accessing the correct file when we navigate to it later.

In the list on the left side of IIS Manager, expand the entry for your server, and then right-click the **Sites** folder and select **Add Website**. In the window that appears, give your website a name and a path. I'm going to point it at the folder I created at `C:\inetpub\example` for this website. Lastly, I'm going to configure the binding for the site by entering the host name I'd like to use for this website. I'm going to use `example.local` for this website. Finally, I'll click **OK** to create the site.

Once the site is created, I can open up a web browser and navigate to `http://localhost` to see what the web server shows. Unfortunately, right now it just shows the default IIS page that we've seen before. This is because we still have the default site enabled on our system. If we try to navigate to `http://example.local` to access our site, that doesn't work either. This is because our web browser will try to use DNS to look up that website, but currently `.local` is not a valid TLD. So, to test this website, we'll need to edit our `hosts` file on Windows to include an entry for our test website.

The simplest way to edit the `hosts` file on Windows is to first open **Notepad** as administrator. Next, click **File** and then **Open**, and navigate to `C:\Windows\System32\drivers\etc` and change the view to show all files. You should see a file named `hosts` in that directory. As a quick sidenote, this directory's name, `etc`, is directly related to the `etc` folder on Linux-based systems that stores many of these same files.

In that file, simply add a new line at the bottom for our new website:

```
127.0.0.1   example.local
```

Then, save and close the file. Finally, in your web browser, try once again to visit `http://example.local`. This should take you directly to your new website.

In effect, what the `hosts` file does is override the DNS system on your computer. Before looking up an address via DNS, your computer will check the hosts file for any entries matching that domain name. This is a direct throwback to the `hosts.txt` file discussed in Module 3 when we first introduced DNS. Then, just like Apache does with virtual hosts, IIS will examine an incoming request and determine which domain name is requested. It will then compare that to the bindings for the various websites on the server, and respond with the appropriate site that matches the request. This is a great way to test these features without having to set up a full DNS server in our development system.

Next, let's configure this website to use a secure connection and a public key certificate. Back in IIS Manager, select the server in the list of items on the left side, then open the **Server Certificates** option to the right. Here, I can click the **Create Self-Signed Certificate** option on the right-hand side to create a new certificate for our server. In the window that appears, I can give the certificate a name. In this case, I'll just use the name of my website, `example.local`. That's all it takes! We now have certificate we can use.

Next, we'll need to assign it to our site. To do this, right-click on your site in the left-hand list in IIS Manager, and select **Edit Bindings**. There, we'll add a new binding for type "https" and the same host name as before. Finally, at the bottom, we can select the certificate we just created as the security certificate for this website. Finally, click **OK** to save those changes.

We can test those settings by opening a web browser and navigating to `https://example.local`. However, at this point, most web browsers will complain about the connection being insecure. This is a bit misleading, as the connection will be properly encrypted just fine. However, since your browser cannot establish a chain of trust for the certificate, it is warning you that the website could be compromised and a malicious third-party could be on the other end of your connection. In this case, we know that the connection is safe, so I'll just click the option to add a security exception for this site. That should allow you to see the website once again, this time via HTTPS.

Finally, let's configure this website to automatically redirect users from HTTP to HTTPS, just like we've done previously with Apache using Certbot. There are many ways to do this, but one of the simplest is to install the "URL Rewrite" module for IIS. I'll be closely following the guide from Namecheap that is linked in the resources section below the video, so feel free to refer to it as well for screenshots of this process.

First, I'll need to download and install the module. You can also find it linked in the resources section below this video. Once it is installed, you'll need to close and reopen IIS Manager. Now, if you select your site in the list on the left, you should see a new **URL Rewrite** option in the list of icons. To add a rule, double-click that icon to open its settings, then click the **Add Rules** option to the right.

From here, you should be able to follow the guide from Namecheap to set up the redirect rule. I won't demonstrate that full process here, as you'll need to do that as part of your lab assignment.

Now, let's test this setup. First, clear the cache of the web browser you are using for testing, just to be sure that we aren't still reading any cached information from that site. Then, navigate to `http://example.local`, and hopefully you should be redirected to `https://example.local` automatically.

As you can see, working with IIS is very similar to working with Apache. Some things are a bit easier to configure in IIS, while others are simpler in Apache in my opinion. Thankfully, many of the concepts are the same across all web browsers, so it is easy to adapt your knowledge to fit the current software you are using.

In the next video, I'll discuss the steps for installing a .NET web application on this server.
