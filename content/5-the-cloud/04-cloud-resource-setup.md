---
title: "Cloud Resource Setup"
weight: 20
pre: "4. "
---

{{% notice note %}}
TODO _This video was recorded for Ubuntu 18.04, but works for Ubuntu 20.04 as well. When creating a droplet, simply select the newest version of Ubuntu LTS. This video shows an older version of the DigitalOcean UI, but should be similar to what you see today. --Russ_
{{% /notice %}}

{{< youtube UfqT889Vp2I >}}

#### Resources

* **[Slides]({{< relref "/5-the-cloud/04-cloud-resource-setup-slides.md" >}})**
* **[Student Developer Pack](https://education.github.com/pack) from GitHub Education**
* **[Referral Program](https://www.digitalocean.com/referral-program/) from DigitalOcean**
* **[Extras - SSH]({{< relref "/X-extras/02-ssh" >}})**
* **[Extras - Windows Subsystem for Linux]({{< relref "/X-extras/06-windows-subsystem-for-linux" >}})**
* [How to Create a Droplet from the DigitalOcean Control Panel](https://www.digitalocean.com/docs/droplets/how-to/create/) from DigitalOcean
* [An Introduction to Cloud-Config Scripting](https://www.digitalocean.com/community/tutorials/an-introduction-to-cloud-config-scripting) from DigitalOcean
* [Initial Server Setup with Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-20-04) from DigitalOcean
* [Virtual Private Cloud (VPC)](https://www.digitalocean.com/docs/networking/vpc/) from DigitalOcean (replaced private networking)
* [UFW Essentials: Common Firewall Rules and Commands](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands) from DigitalOcean
* [How Does SSH Work](https://www.hostinger.com/tutorials/ssh-tutorial-how-does-ssh-work) from Hostinger
* [SSH Essentials: Working with SSH Servers, Clients and Keys](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys) from DigitalOcean
* [How to Set Up SSH Keys on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-20-04) from DigitalOcean
* [Simplify Your Life With an SSH Config File](https://nerderati.com/2011/03/17/simplify-your-life-with-an-ssh-config-file/) from Nerderati
* [How To Add Swap Space on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-20-04) from DigitalOcean _(not recommended)_

#### Video Transcript

For the rest of this module, you'll be working with DigitalOcean to create and configure online cloud resources. I chose DigitalOcean primarily because of its ease of use compared to other providers such as AWS, as well as its continuing popularity and great user documentation.

DigitalOcean was first founded in 2011 by Ben and Moisey Uretsky. They felt that most hosting companies of the time were targeting large enterprises, leaving many smaller software developers and startups behind. DigitalOcean was one of the first hosting providers to offer virtual machines exclusively on solid state storage, giving them a performance edge over many of their peers, while often being cheaper overall. Currently, they are the 3rd largest hosting provider in the world, with 12 worldwide datacenters serving over 1 million customers.

In this video, we'll discuss the first steps for getting your first cloud server, referred to as a "droplet" on DigitalOcean, configured and secured. Let's get to it!

First, if you haven't signed up for the GitHub Education Student Developer Pack, I highly encourage you to do so. Among many other perks included in the pack is a $50 credit for new DigitalOcean users. So, if you haven't used DigitalOcean before, or would like to create a new account for this class, you should take advantage of that resource. In total, the entire class should use less than half of that credit as long as you don't get behind, so you'll have plenty left over for other projects. Finally, if you have a friend or colleague already using DigitalOcean, you can contact them for their referral URL before you sign up to do them a solid favor, netting you a $10 sign-up credit, and they'll get a $25 credit once you spend $25 at DigitalOcean. It's a win-win for everyone involved!

Once you are logged in, you'll be ready to create your first droplet. I'm going to walk through the steps here and talk through some of the options, just so you know what is available here.

First, you'll be prompted to select an image. DigitalOcean offers many different types of images, including Linux distributions, containers, and one-click applications. The last two options are really handy if you need just a particular service or type of machine, but in our case, we'll select the Ubuntu distribution. Currently, DigitalOcean offers all LTS versions of Ubuntu that are still supported. We'll choose the "Ubuntu 20.04 x64" option.

Next, you'll need to select a droplet size. Droplets on DigitalOcean are sized by the amount of memory they offer, as well as the number of virtual CPUs available and the size of the storage disk. There are many different options to fit a variety of needs. For this class, we'll select the cheapest option, which has 1 GB of memory, 1 virtual CPU, and 25 GB of storage space. It is more than enough for our needs, and only costs $5/month.

DigitalOcean also provides the option to have automatically created backups of your droplets for just an additional fee. I won't enable that option, but you are welcome to do so if you'd like to have that feature available.

Similarly, they also offer the ability to have your storage volumes separate from your droplets. This is handy if you'll be building or rebuilding your droplets and want to make sure the stored data is unaffected. We won't be using this option for this course.

Below that, you'll be able to choose your datacenter region. In general, it is best to select a region close to you and where you'll be accessing these droplets. So, I'd recommend selecting one of the New York or San Francisco options. If you are creating multiple droplets, as you will for this class, make sure they are in the same datacenter region so they are able to communicate with one another internally.

There are a few other options you can enable. The first is private networking, which allows droplets in the same datacenter region to communicate on a private network that is internal to DigitalOcean's datacenter. This is great if you'll be storing data on one droplet and accessing it via another, as you use the private network to protect that connection from eavesdropping.

{{% notice note %}}

Private networking has been replaced by Virtual Private Cloud (VPC) networking, but it works effectively the same.

{{% /notice %}}

Next, you can enable IPv6 access to the droplet. Depending on your network infrastructure, you may or may not find this useful. We won't be enabling it in this course.

The user data option allows you to provide some initial configuration information to your droplet using the `cloud-init` program. If you are creating many droplets from scratch that all need the same configuration, this can be a very powerful tool. However, for this course we'll be performing our configuration manually, so we won't be using this right now.

Finally, DigitalOcean offers advanced droplet monitoring at no extra charge. Let's enable that option here, and later we'll look at the information it collects for us.

You can also add SSH keys directly to your droplet. If you do so, the system will be configured to prevent SSH login via password, and you won't receive the root password via email from DigitalOcean. If you have already configured an SSH key with DigitalOcean, you can add it to your droplet here, but if not, I'll walk you through the steps to do that later in this video.

Lastly, you can create multiple droplets with the same settings. For the lab, you'll need to create two droplets, named **FRONTEND** and **BACKEND**. For this example, however, I'm just going to create one, and name it **EXAMPLE**. As part of the lab, you'll have to extrapolate what I demonstrate here on a single droplet to your setup with multiple droplets.

Finally, I can click the "Create" button to create my droplet. After a few seconds, you should see the IP address of your droplet in your dashboard. Let's click on it to see additional information about the droplet.

At the top of the page, you'll see your droplet's public IP address, as well as the private IP address for the internal network. Notice that the private IP address begins with a 10, which is one of the reserved network segments we discussed in Module 3. On the left of the page, you'll see several options you can explore. For example, clicking the "Access" option will allow you to launch a virtual console to connect to your server. This is very handy if you accidentally lock yourself out of the droplet via SSH. Of course, you'll need to actually know a password for an account on the system to log in via the console. Thankfully, if you forget your root password, there is a button below to reset that password and have it emailed to you.

For this example, however, let's use SSH to connect to our droplet. I'm going to use one of my Ubuntu VMs from the earlier labs for this process, but you are welcome to use tools from your own host machine instead of running it in a VM. Mac and Linux users have easy access to SSH via the terminal already. For Windows users, I recommend using the Windows Subsystem for Linux to get access to SSH through Ubuntu installed directly on Windows. See the video on WSL in the Extras Module for more information on installing and configuring that application.

To connect, you'll use a command similar to this one:

```bash
ssh root@<ip_address>
```

where `<ip_address>` is the public IP address of your droplet. When prompted, use the password for the `root` account you should have received via email from DigitalOcean. If everything works correctly, you should now be logged in as the `root` user of your droplet.

Of course, if you've been paying attention to this class, you should know that it is a very bad idea to use the `root` account directly on a system. That goes double for working in the cloud! So, the first thing we should do is create a new user named `cis527`. As you'll recall from Module 1, you can do so using the `adduser` command:

```bash
adduser cis527
```

It will ask you a few simple questions about that user, and then create that user for you. You'll need to also give that user administrative privileges:

```bash
usermod -a -G sudo cis527
```

Once that is done, we should log out of the `root` account and log in as the new account. So, let's exit for now:

```bash
exit
```

Back on our local machine, we'll need to set up some SSH keys so that we can log in securely. If you'd like to learn more about this process, please review the SSH video in the Extras Module.

First, if you haven't already, you'll need to create a set of SSH keys on this system:

```bash
ssh-keygen -t rsa -b 4096
```

Then, once the key is created, you can copy it to your DigitalOcean droplet using a command similar to this:

```bash
ssh-copy-id cis527@<ip_address>
```

where `<ip_address>` is the public IP address of your droplet. You'll be asked to provide the password for the `cis527` account you just created, and then it will install your SSH key for that user. Finally, you can log in to the system using SSH:

```bash
ssh cis527@<ip_address>
```

If everything works correctly, you should not be asked for your password at all, unless you put a passphrase on your SSH key. Of course, at this point you could also create an SSH config file to make this process even easier - the SSH video in the Extras module has details for how to go about doing that.

Once you've created your new user and switched to that account, there are a few important security steps you should take to make sure your droplet is properly secured. First, you should configure the firewall to only allow the ports you intend to use on this system. For example, you might allow port `80` for HTTP traffic, port `443` for HTTPS traffic, and port `22` for SSH traffic. In addition, you could restrict the IP addresses that are able to access certain ports. For this example droplet, I'm going to enable those three ports:

```bash
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443
```

Then, I can enable the firewall:

```bash
sudo ufw enable
```

and check the status using:

```bash
sudo ufw status
```

For the lab assignment, your firewall configuration will be a bit more complex, so make sure you read the assignment carefully before enabling the firewall. If you end up locking yourself out of the system, remember that you can use the console through the DigitalOcean website to get in and fix problems with your firewall configuration.

In addition, I recommend securing your SSH server by disabling password authentication and root login. You can do so by editing the SSH configuration file:

```bash
sudo nano /etc/ssh/sshd_config
```

SSH servers on the internet receive sometimes hundreds or event thousands of login attempts per day from hackers trying to exploit systems with weak passwords. If your system doesn't even accept passwords, it is just one less way they can potentially get in.

Also, you can change the port that the SSH server is listening on. This is a little bit of "security by obscurity," which isn't really security by itself, but it can definitely help cut down on those malicious login attempts. The lab assignment directs you to do just this. Of course, make sure you update your firewall configuration accordingly when you make this change. Once you've made your changes, you can restart the SSH server:

```bash
sudo systemctl restart ssh
```

Lastly, you may want to perform steps such as updating the timezone of your server and configuring the Network Time Protocol (NTP) client to make sure the system's time is synchronized properly.

One other step that you may come across in many guides is enabling swap. Swap in Linux allows you to effectively use more RAM than what is available on your system. This is especially handy if you are dealing with large datasets that won't fit in RAM. The desktop version of Ubuntu typically does this automatically, but many cloud providers such as DigitalOcean disable this feature. Since they are in the business of providing cloud resources, in general they will just want you to scale your resources accordingly to have enough RAM available instead of using swap. In addition, using swap on a solid-state drive can degrade performance and shorten the life of the drive. So, I don't recommend enabling swap on your DigitalOcean droplets at all, unless you find a particular use case that would make it worthwhile.

With that information, you should be ready to configure and secure your first cloud server. Next, we'll look at how to access a cloud resource using a domain name and configuring that resource accordingly.
