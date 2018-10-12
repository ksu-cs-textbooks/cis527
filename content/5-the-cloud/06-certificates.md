---
title: "Certificates"
weight: 30
pre: "6. "
---

{{< youtube  >}}

#### Resources

* **[Slides]({{< relref "/5-the-cloud/06-certificates-slides.md" >}})**
* **[Core Networking Services - Security]({{< relref "/3-core-networking-services/15-security" >}})**
* [Public Key Certificate](https://en.wikipedia.org/wiki/Public_key_certificate) from Wikipedia
* [Certbot](https://certbot.eff.org/) from the Electronic Frontier Foundation (EFF)
* [How To Secure Apache with Let's Encrypt on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-18-04) from DigitalOcean

#### Video Transcript

So far, we've created a cloud server, a domain name, and connected the two so our users can access our cloud resources. However, we haven't done anything to secure the connection between our users and our cloud system, which means that any information sent via HTTP to and from our server can be intercepted and read by a malicious third party. As you'll recall, in Module 3 we showed how simple it is to do just that using Wireshark.

To secure our connections, we want to use HTTPS, which is simply HTTP using TLS to create a secured and encrypted tunnel. We've already discussed TLS a bit in Module 3, so feel free to refer to that video if you need a quick refresher of what TLS is and how it works.

As part of the TLS handshake, each system exchanges security information, such as a public key certificate, that is used to verify each other's identity and construct a shared encryption key for the connection. It is very simple to create one of those certificates on your system, and then instruct your web server to use that certificate to create a secure connection. Those certificates are sometimes referred to as "SSL Certificates" or "TLS Certificates" as well.

However, since you created that certificate yourself, it is known as a "self-signed" certificate, and really can't be used to confirm your identity directly. For example, you could easily create a certificate that says this system is the server for `amazon.com`, but that wouldn't be true. So, how can we use those certificates to confirm a system's identity?

The solution is to use a "chain of trust" to verify the certificate. Each web browser and operating system has a set of root certificates installed which belong to several trusted entities, called certificate authorities, or CAs, from across the world. They, in turn, can issue intermediate certificates to others acting on their behalf. To validate that intermediate certificate, the root CA signs it using their own certificate. This signature can easily be verified to make sure it is genuine. Then, the intermediate certificates can be used to sign certificates for a website or cloud resource.

When your web browser receives a certificate from a website, it can look at the signatures and verify the "chain of trust" that authenticates the certificate. In most web browsers, you can view this information by clicking on the lock icon next to the URL in the address bar. For example, the certificate for Wikipedia is currently signed by a certificate from "GlobalSign Organization Validation CA," which in turn is signed by the "GlobalSign Root CA" certificate.

In essence, your web browser says "Well, I trust GlobalSign Root CA's certificate, and they say they trust GlobalSign Organization Validation CA's certificate, and the Wikipedia certificate was signed by that certificate, so it must be correct."

So, as the administrator of resources in the cloud, it is in your best interest to not only use HTTPS to secure your web traffic, but you should also provide a valid certificate that has been signed by a trusted root CA. This helps ensure that your users can trust that the system they are connecting to is the correct one.

Unfortunately, obtaining certificates could be expensive in the past, depending on your needs. Many times you would need to obtain these certificates through your domain registrar, or directly from a variety of certificate authorities on the internet. While those are still options, and in many cases for a large enterprise they are the best options, there is a better way for us to secure our websites.

The Internet Security Research Group created Let's Encrypt, a free certificate authority that allows the owner of a domain name to request a security certificate free of charge. To make it even easier, the Electronic Frontier Foundation, or EFF, created Certbot, a free tool that helps you configure and secure your websites using Let's Encrypt. So, let's see how easy it is to do just that on our cloud server.

I'm going to quickly walk through the DigitalOcean guide for using Let's Encrypt on Apache, which is linked below this video in the resources section. Feel free to refer to that guide for additional information and discussion about this process.

First, I'll need to install Certbot by adding the appropriate APT repository and installing the package:

```bash
sudo add-apt-repository ppa:certbot/certbot
sudo apt install python-certbot-apache
```

Next, I'll need to make sure that the configuration file for my website is stored correctly and has the correct information. For example, if the website I would like to secure is `foo.russfeld.me`, my configuration file should be stored in `/etc/apache2/sites-available/foo.russfeld.me.conf`, and inside that file should be a line for `ServerName foo.russfeld.me`. Make sure that all three are correct before continuing.

In addition, you'll need to make sure your firewall is configured to allow HTTPS traffic on port 443 through the firewall.

Finally, you can use Certbot to request a certificate for your website. For my example site, the command would be this:

```bash
sudo certbot --apache -d foo.russfeld.me
```

If you'd like to create a certificate for more than one website, you can include them with additional `-d` flags at the end of this command.

Certbot may ask you a few questions as it requests your security certificates, including your email address. At the end, it will ask you to choose if you'd like to have your site automatically redirected to HTTPS. I always recommend enabling this option, so that anyone who visits your site will be automatically secured.

That's all there is to it! At this point, I recommend clearing the cache in your web browser to make sure it doesn't have any cached information from that website. Then, you can visit your website in your browser, and it should automatically redirect you to the HTTPS protocol. You can then examine the certificate to make sure it is valid.

There is really no excuse in this day and age for having a website without a valid, authenticated security certificate, since it is so simple and easy to do. As a system administrator, you should strive to make sure every system you manage is properly secured, and this is one important part of that process.
