---
title: "Domains & Virtual Hosts"
weight: 25
pre: "5. "
---

{{< youtube mPlPMOpnvjE >}}

#### Resources

* **[Slides]({{< relref "/5-the-cloud/05-domains-virtual-hosts-slides.md" >}})**
* **[Core Networking Services - DNS]({{< relref "/3-core-networking-services/11-dns" >}})**
* **[Student Developer Pack](https://education.github.com/pack) from GitHub Education**
* [How To Install the Apache Web Server on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04) from DigitalOcean
* [DNS Overview](https://www.digitalocean.com/docs/networking/dns/overview/) from DigitalOcean
* [How to Point to DigitalOcean Nameservers from Common Domain Registrars](https://www.digitalocean.com/community/tutorials/how-to-point-to-digitalocean-nameservers-from-common-domain-registrars#registrar-namecheap) from DigitalOcean

#### Video Transcript

Now that you've set up and configured your first cloud server, let's discuss how to make that resource easily accessible to you and your organization.

In Module 3, we discussed the Domain Name System, or DNS, as the "phonebook of the internet." It contains a list of domain names and the associated IP addresses for each one. We already have the IP address of our cloud server, now we must add our own entry to the domain name space as well.

When you register for a domain, you'll typically be registering for a second-level domain name, which is one step below a top-level domain, or TLD, such as `.com`, `.org`, and `.net`, among others. In this example, `wikipedia` is the second-level domain name below the `.org` TLD.

To see it a bit more clearly, here is a diagram showing the breakdown of a common web Uniform Resource Locator, or URL. A URL is written with the top-level domain at the end, and then working backwards to forwards you can see the full hierarchy of the address in the domain name space. At the front is the protocol used to access that resource. In our case, we'll be registering a domain name, and then creating a few subdomains for our cloud resources.

For this lab assignment, you'll be asked to register a domain name. I'll be using Namecheap for my example website, since it is the domain registrar I've been using for my personal sites for some time. There are many other registrars out there on the internet, and each one offers different services and prices. You are welcome to use any registrar you like for this lab. Once again, the GitHub Student Developer Pack is an excellent resource, and one of the discounts offered is a free `.me` domain through Namecheap for one year. Honestly, if you don't already have a personal domain name, now is a great time to register one!

When registering a domain name, the most important thing to think about, first of all, is the name itself. Most domain registrars offer a search feature to see which domains are available and what the price is. You'll also notice that the same domain name may be offered for wildly different prices under different TLDs. So, you'll have to consider your choice of name and TLD carefully.

In addition, you can register the same second-level domain name under a variety of top-level domains, though each one comes at an addition cost, both in terms of price and management. Many large enterprises choose to do this to prevent "cybersquatting," where another user registers a similar domain name, hoping to profit on it in some way. For example, Google owns many different domain names related to `google.com`, including `gogle.com`, `goolge.com`, and `googlr.com` in order to make sure that users who type the domain name slightly incorrectly still reach the correct website.

Once you've purchased your domain name, you'll have a choice of how the DNS configuration is hosted. For many users, they are only planning on using the domain name with a particular website hosting service, such as WordPress or GitHub Pages. In that case, you can set up your domain to point to your host's nameservers, and they'll manage everything for you.

However, you may want to use this domain name for a variety of uses. In that case, I highly recommend managing your DNS settings yourself. You can choose to use your registrar's built-in DNS hosting, which is what I'll do in this example. Many cloud providers, such as DigitalOcean, also offer a hosted DNS service that you can use for this feature. In general, I've always kept my domain names and cloud hosting separate, just to add a bit more resiliency in case one provider or the other has a problem.

Finally, whenever you register a domain name, you are legally required to provide contact information, including your name, mailing address, and phone number, for the Whois service, a public service that provides information about all registered domains. In many cases, that would be your own personal information, which would be posted publicly along with the domain name by your registrar. For many individuals, that could create a major privacy and identity theft concern.

Thankfully, many domain registrars offer a privacy service that will replace your contact information with their own in the Whois database. In essence, they post their information publicly on your behalf, and then they will send any official communication to you directly. It helps prevent your personal information from being publicly available. In the case of Namecheap, their WhoisGuard service does just that, and as of this writing it is available free of charge for any users who register a domain name through their service. I highly recommend using one of these services to protect your private information when you register a domain name for your own personal use.

Let's take a look at how to register and configure a domain name. As I mentioned, I'll be using Namecheap for this example, but there are many other registrars out there that you can use. First, I'll use their domain name search tool to see if a particular domain name is available. Let's search for `cis527` and see what's out there.

As you can see, that domain name is available on a variety of TLDs, and at a variety of prices as well, ranging from less than $1 to more than $60 per year. The price can fluctuate wildly depending on the demand and popularity of a particular TLD. Once you choose your domain name and TLD, you can work through your registrar to register and pay for the domain. You'll also be asked to provide them with the appropriate information for the Whois service.

Once you've registered your domain name, you can usually configure it through your registrar's website. Most importantly, you'll be able to define where the nameservers for your domain are located. As we discussed above, I recommend using your registrar's nameservers or the nameservers of your cloud provider so you can manage the DNS settings yourself. If you are using a particular website hosting service, they may have instructions for configuring this section to point to their nameservers.

Since I'm using Namecheap's DNS service, I can view the DNS settings right here as well. Looking at these settings, you'll see that I have several A records already configured for this domain name. Each of these A records could point to a different cloud resource or server that I manage. However, you'll notice that they all point to the same IP address. So, what's going on here?

On my cloud server, I'm using the Apache web server. You'll be using the same software on your own servers in the lab assignment. Thankfully, Apache, as well as most other web servers, has a unique feature that allows you to host multiple websites on the same IP address. This allows you make much more efficient use of your resources. Instead of having one droplet per website you manage, you can host many websites on the same droplet, and they can all share the same computing resource and bandwidth. If you are only hosting very small websites that don't get much traffic, this is a great option.

In Apache, you can do this by configuring "virtual hosts" on the server. A virtual host defines a domain name and matches it with a folder storing the website's files. When an incoming request comes to the server, it analyzes the domain name requested in the packet, and then finds the appropriate website to display. Because of this, it is very important to have your DNS settings set correctly for your domain. If you try to access this server by its IP address alone, you'll generally only be able to see one of the websites it has available.

To configure your system to use virtual hosts, there are a couple of steps. First, in your DNS configuration, you'll need to add new A records for each website you'd like to host. For this example, I'll just use the names `foo` and `bar`. In each A record, I'll set the IP address to be the public address of my web server.

Once I save my changes, that record will be updated in my registrar's DNS servers. However, due to the large amount of caching and redundancy in the worldwide DNS network, it could take up to 24 hours for the changes to fully propagate. In general, you can avoid some of those issues by restarting your system to clear the DNS cache, using 3rd party DNS servers such as OpenDNS or Google DNS, and not querying this DNS entry right away so that the DNS servers don't cache an invalid entry. However, in many cases you'll simply have to wait until it starts working before you can continue, and there isn't a whole lot you can do to make it go faster.

Next, on my DigitalOcean droplet, I'll install Apache if I haven't already:

```bash
sudo apt update
sudo apt install apache2
```

and then create a folder to store the first website:

```bash
sudo mkdir -p /var/www/foo/html
```

To make it really simple to see which website is which, I'll simply place a file that folder, giving the name of the site:

```bash
sudo nano /var/www/foo/html/index.html
```

Now, I'll need to configure a virtual host file for that website:

```bash
sudo nano /etc/apache2/sites-available/foo.russfeld.me.conf
```

The `/etc/apache2/sites-available/` directory stores all of the available site configuration files for Apache by convention. Of course, you'll need to update the filename to match your domain name. In that file, I'll place the following information, which I've adapted from the DigitalOcean guide on installing Apache linked in the resources section below this video:

```apache
<VirtualHost foo.russfeld.me:80>
    ServerAdmin admin@russfeld.me
    ServerName foo.russfeld.me
    DocumentRoot /var/www/foo/html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

Then, I'll save and close the file. Finally, I'll need to deactivate the default website, and activate the new site:

```bash
sudo a2dissite 000-default
sudo a2ensite foo.russfeld.me
```

Once I've activated it, I can check for any configuration errors:

```bash
sudo apache2ctl configtest
```

If it passes, I can restart the Apache service to reload my changes:

```bash
sudo systemctl restart apache2
```

I'll do these same steps for the other site, named `bar`, as well. The DigitalOcean guide for installing Apache includes much more in-depth information about this process, so I encourage you to read it carefully to learn even more about how to configure and work with Apache.

Once I've done that, I can test my virtual host configuration and see if it works. To do this, I'll open a web browser and navigate to `http://foo.russfeld.me` and see if it takes me to the correct website. I can also try `http://bar.russfeld.me` to test the other website. As you can see, they both work correctly.

This is just a brief introduction to setting up your own domain name and configuring your cloud resources to use that domain. In the next few lab assignments, you'll be configuring several virtual hosts similar to these. If you run into issues getting it to work, I encourage you to post a question in the course discussion forums.
