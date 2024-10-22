---
title: "Assignment"
weight: 15
pre: "3. "
---

### Lab 5 - The Cloud

#### Instructions

Create **two** cloud systems meeting the specifications given below. The best way to accomplish this is to treat this assignment like a checklist and check things off as you complete them.

If you have any questions about these items or are unsure what they mean, please contact the instructor. Remember that part of being a system administrator (and a software developer in general) is working within vague specifications to provide what your client is requesting, so eliciting additional information is a very necessary skill.

{{% notice note %}}
_To be more blunt - this specification may be purposefully designed to be vague, and it is your responsibility to ask questions about any vagaries you find. Once you begin the grading process, you cannot go back and change things, so be sure that your machines meet the expected specification regardless of what is written here. --Russ_
{{% /notice %}}

Also, to complete many of these items, you may need to refer to additional materials and references not included in this document. System administrators must learn how to make use of available resources, so this is a good first step toward that. Of course, there's always [Google](http://www.google.com)!

#### Time Expectation

This lab may take anywhere from **1 - 6 hours** to complete, depending on your previous experience working with these tools and the speed of the hardware you are using. Configuring cloud systems is very time-consuming the first time through the process, but it will be much more familiar by the end of this course.

{{% notice info %}}
_This lab involves working with resources on the cloud, and will require you to sign up and pay for those services. In general, your total cost should be low, usually around $20 total. If you haven't already, you can sign up for the [GitHub Student Developer Pack](https://education.github.com/pack) to get discounts on most of these items._

_You can get $200 credit at DigitalOcean using this link: [https://try.digitalocean.com/freetrialoffer/](https://try.digitalocean.com/freetrialoffer/)_

_You can register a .me domain name for free using Namecheap at this link: [https://nc.me/](https://nc.me/)_

_If you have any concerns about using these services, please contact me to make alternative arrangements! --Russ_
{{% /notice %}}

---

### Task 0: Create 2 Droplets

Create **TWO** droplets on DigitalOcean. As you set up your droplets, use the following settings:

* Choose the Ubuntu 24.04 x64 distribution as the droplet image
* Select the smallest droplet size ($4-6/mo - you may have to click around and click an arrow to see the smallest option)
* Select any United States region - make sure both are in the same region!
* Enable Virtual Private Cloud (VPC) Networking and Monitoring (this should be the default)
* You may add any existing SSH keys you've already configured with DigitalOcean during droplet creation
* Droplet names:
  * `cis527<your eID>-frontend`
  * `cis527<your eID>-backend`

The rest of this assignment will refer to those droplets as **FRONTEND** and **BACKEND**, respectively.

#### Resources

* [How to Create a Droplet from the DigitalOcean Control Panel](https://www.digitalocean.com/docs/droplets/how-to/create/) from DigitalOcean
* [Virtual Private Cloud (VPC)](https://www.digitalocean.com/docs/networking/vpc/) from DigitalOcean (replaced private networking)
---

### Task 1: Configure Droplets

Perform these configuration steps on both droplets, unless otherwise noted:

1. Create a cis527 user with administrative (root or sudo) privileges
{{% notice warning %}}
**DO NOT REUSE THE USUAL PASSWORD ON THIS ACCOUNT!** Any system running in the cloud should have a very secure password on each account. Make sure it is a strong yet memorable password, as you'll need it to run any commands using `sudo`.
{{% /notice %}}
1. Install all system updates
1. Ensure the timezone is set to UTC
1. Enable the firewall. Configure the firewall on both systems to allow connections to the following:
   * incoming port 22 (SSH)
       * **BACKEND ONLY:** filter connections on port 22 to only allow SSH connections from **FRONTEND** via its **private networking** IP address. You should still allow connections to port 80 and 443 from any address.
   * incoming port 80 (HTTP)
   * incoming port 443 (HTTP via TLS)

{{% notice warning %}}

_Many students misconfigure the firewall on the **BACKEND** server to allow SSH connections from the wrong IP addresses or ranges, or include a rule to allow connections from any address. I will be picky about this from now on. --Russ_

{{% /notice %}}

#### Resources

* [Initial Server Setup with Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-22-04) from DigitalOcean (works for 24.04)
* [UFW Essentials: Common Firewall Rules and Commands](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands) from DigitalOcean
* [How To Set Up Time Synchronization on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-time-synchronization-on-ubuntu-20-04) from DigitalOcean (works on Ubuntu 22.04)

---

### Task 2: SSH Configuration

Configure your SSH servers and SSH keys as described here:

1. On your own computer, generate a set of SSH keys if you have not already.
2. Add the public key from your computer to the cis527 account on **FRONTEND**. This should allow you to log in with that key.
3. Add the [grading SSH key](files/id_rsa_grading.pub) to the cis527 account on **FRONTEND** as well.
4. On the cis527 account on **FRONTEND**, generate a set of SSH keys with no passphrase.
5. Add the public key from the cis527 account on **FRONTEND** to the cis527 account on **BACKEND**. This should allow you to log in with that key
6. On the cis527 account on **FRONTEND**, create an SSH config file such that a user could simply type `ssh backend` to connect to the **BACKEND** droplet.
{{% notice tip %}}
Make sure you use the private networking IP address for **BACKEND** in your config file. Otherwise, it will be blocked by the firewall.
{{% /notice %}}
7. Once all of the keys are in place, disable password authentication and root login via SSH on both systems.

After doing these steps, you should only be able to access the cis527 account on **FRONTEND** via SSH using your SSH key or the grading SSH key, and you should only be able to access **BACKEND** using the SSH key present on the cis527 account on **FRONTEND**.

{{% notice note %}}
_You may contact me once you have installed the grading SSH key to confirm that it works correctly. I'd be happy to test it before grading. --Russ_
{{% /notice %}}

{{% notice note %}}
If you are working on campus, you will not be able to use SSH to connect to your **FRONTEND** droplet since outgoing SSH is blocked by K-State. The ability to log in via SSH to **FRONTEND** using your key will not be graded, but we'll use the grading key for testing on our end. 

Instead, you can use the Access tab in DigitalOcean to access a virtual console for your droplet. This allows you to connect via SSH through a web browser.

You should ensure that you can access the **BACKEND** server from **FRONTEND** using SSH with the correct SSH keys.
{{% /notice %}}

#### Resources

* **[Extras - SSH]({{% relref "/X-extras/02-ssh"  %}})**
* [How Does SSH Work](https://www.hostinger.com/tutorials/ssh-tutorial-how-does-ssh-work) from Hostinger
* [SSH Essentials: Working with SSH Servers, Clients and Keys](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys) from DigitalOcean
* [How to Set Up SSH Keys on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-22-04) from DigitalOcean
* [Simplify Your Life With an SSH Config File](https://nerderati.com/2011/03/17/simplify-your-life-with-an-ssh-config-file/) from Nerderati

---

### Task 3A: Install Apache on **BACKEND**

Install the Apache web server on **BACKEND**. By default, the webserver should serve files from the `/var/www/html` directory. Place a simple HTML file named `index.html` in that directory on **BACKEND**. You may use the contents below as an example. Please modify the file appropriately to make it clear which server it is placed on.

Do not configure virtual hosts at this time, as that will be covered in Task 5.

```html
<html>
    <head>
        <title>CIS 527 Backend</title>
    </head>
    <body>
        <h1>This is my CIS 527 Backend Server!</h1>
    </body>
</html>
```

To test your system, you should be able to enter the public IP address of your **BACKEND** droplet in a web browser and be presented with the appropriate file.

#### Resources

* [How To Install the Apache Web Server on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-22-04) from DigitalOcean

---

### Task 3B: Install Docker on **FRONTEND**

Install the Docker client, Docker engine, and Docker compose on the droplet named **FRONTEND**. Make sure you test your setup using the [Hello World](https://hub.docker.com/_/hello-world) image to confirm it is working.

#### Resources

* [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/) from Docker
* [Install Docker Compose Plugin](https://docs.docker.com/compose/install/linux/) from Docker

---

### Task 4: Domain Names & DNS

Register and configure a domain name, and add your new droplets to that domain.

{{% notice info %}}
_If you already have your own domain name, you are welcome to use it for this portion of the lab. It should not conflict with any existing configuration, as long as you are managing your own DNS records. If not, you may need to perform some additional configuration. If you don't have a domain name yet, this would be a great chance to get one registered. [Namecheap](https://nc.me) will allow you to register a `.me` domain for free for one year as a student. If you register a domain name, I highly recommend enrolling in WhoisGuard to protect your personal information. It should be enabled for you automatically through Namecheap. If you have any concerns about registering a domain name, or would like to explore options for completing this portion without registering or using a public domain name, please contact me. --Russ_
{{% /notice %}}

Configure the DNS settings for your domain name as follows:

1. If you are using a new domain, make sure it is configured to use your registrar's DNS servers. You may also configure it to use DigitalOcean's nameservers, and configure your DNS settings through DigitalOcean.
1. Add an A record for host `cis527alpha` that points to the public IP address of **FRONTEND**.
1. Add an A record for host `cis527bravo` that points to the public IP address of **FRONTEND**.
1. Add an A record for host `cis527charlie` that points to the public IP address of **BACKEND**.

{{% notice tip %}}
_After updating your domain's DNS settings, you may have to wait up to 24 hours for the changes to propagate across the internet due to DNS caching. You may be able to speed this up by restarting your computer and network devices, or by using 3rd party DNS services such as OpenDNS or Google DNS instead of your ISP's DNS servers. However, in most cases it is better to just be patient and wait than to try and get around it. --Russ_
{{% /notice %}}

To test your new DNS settings, you should be able to enter `http://cis527charlie.<yourdomain>.<tld>` in a web browser to access your backend server running Apache. For example, if your domain name is `cis527.me`, you would visit `http://cis527charlie.cis527.me`. Since we haven't configured a server for frontend yet, we aren't able to test it at this time.

#### Resources

* [DNS Overview](https://docs.digitalocean.com/products/networking/dns/) from DigitalOcean
* [How to Point to DigitalOcean Nameservers from Common Domain Registrars](https://www.digitalocean.com/community/tutorials/how-to-point-to-digitalocean-nameservers-from-common-domain-registrars#registrar-namecheap) from DigitalOcean

---

### Task 5A: Configure Apache Virtual Hosts

Now that your domain name is working, configure an appropriate virtual host in Apache on **BACKEND**. In general, you can follow Step 5 of the guide linked below, but replace `example.com` with your server's full domain name, such as `cis527charlie.cis527.me` in the example from Task 4. You'll also need to copy the sample HTML file from Task 3 to the appropriate directory as configured in your virtual host. Make sure you disable the default site configuration when you enable the new site.

Finally, you can test your virtual host configuration using the same URL given in Task 4 above.

#### Resources

* [How To Install the Apache Web Server on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-22-04) from DigitalOcean

---

### Task 5B: Configure Docker Reverse Proxy

On **FRONTEND**, create a `docker-compose.yml` file in the home directory of the `cis527` user that will create the following infrastructure in Docker:

* Set up two Docker containers running simple web servers.
   * You may either use the [whoami](https://hub.docker.com/r/jwilder/whoami) image from the example, or set up two [Nginx](https://hub.docker.com/_/nginx) containers. If you use Nginx, you'll need to configure it to host different static content in each container (so it is easy to tell which one is which). See the documentation for how to set this up. Basically, there needs to be an obvious way to tell that you are reaching the correct container.
   * These containers should only be connected to an internal Docker network. They should **NOT** have direct access to the internet, nor should they have any mapped ports.
* Set up a reverse proxy in Docker to handle connections from the outside world (on port 80) to the appropriate containers.
   * You may use either [Nginx](https://hub.docker.com/_/nginx), [Nginx-proxy](https://hub.docker.com/r/nginxproxy/nginx-proxy), or [Traefik Proxy](https://hub.docker.com/_/traefik) as shown in the lab module.
   * This container should be connected to both the default Docker network as well as the internal network that is connected to the other two containers.
   * You should configure one web server container to have hostname `cis527alpha.<yourdomain>.<tld>` and the other should have `cis527bravo.<yourdomain>.<tld>`. 
   * Once configured, you should be able to visit those URLs in a browser and clearly see information coming from the correct Docker container.

#### Resources

* [Reverse Proxy]({{% relref "/5a-containers/08-reverse-proxy"  %}})

---

### Task 6: Public Key Certificates

Obtain and install a public key certificate for your Apache server on **BACKEND**. The simplest way to do so is to use Certbot from Let's Encrypt.

When you install the certificates, direct Certbot to redirect HTTP traffic to HTTPS for your server.

Once it is complete, you can test your certificates using the same URL given in Task 4 above. It should automatically redirect you from HTTP to HTTPS. You may have to clear the cache in your web browser if it does not work correctly. When you access the site, use your web browser to verify that the SSL certificate is present and valid.

You **DO NOT** have to configure public key certificates on **FRONTEND** using a reverse proxy. This can be done, but it is a bit more difficult than using Certbot since it requires manual steps or additional configuration. Feel free to attempt it on your own!

#### Resources

* [Certbot](https://certbot.eff.org/) from the Electronic Frontier Foundation (EFF)
* [How To Secure Apache with Let's Encrypt on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-22-04) from DigitalOcean

---

### Task 7: Schedule A Grading Time

Contact the instructor and schedule a time for interactive grading. You may continue with the next module once grading has been completed.
