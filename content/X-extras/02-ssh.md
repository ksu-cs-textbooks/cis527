---
title: "SSH"
weight: 10
pre: "2. "
---

{{< youtube 19Fo6yUiPvE >}}

#### Resources

* [How Does SSH Work](https://www.hostinger.com/tutorials/ssh-tutorial-how-does-ssh-work) from Hostinger
* [SSH Essentials: Working with SSH Servers, Clientsand Keys](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys) from DigitalOcean
* [How to Set Up SSH Keys on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-1804) from DigitalOcean
* [Simplify Your Life With an SSH Config File](https://nerderati.com/2011/03/17/simplify-your-life-with-an-ssh-config-file/) from Nerderati

#### Video Transcript

In this video, I'll discuss how to use the Secure Shell, or SSH, remote server and client. You'll be using it throughout the semester to connect to various computers, and there are a few things you should know that will help make your experience a much more pleasant one.

If you'd like to know more about the technical details of how SSH works, refer to the links in the resources section below the video.

First, let's look at the SSH client program, available as the `ssh` command on most Linux systems. It is typically installed by default, but if not you can install it using the `apt` command:

```bash
sudo apt install openssh-client
```

Once it is installed, you can connect to any server you wish by simply using the `ssh` command followed by the host you'd like to connect to. Optionally, you may need to provide a different username, in which case you would put the username before the host, connecting the two with an `@` symbol, much like an email address. If you'd like to try it yourself, you can try to connect to the CS Linux servers using a command similar to the following:

```bash
ssh russfeld@cslinux.cs.ksu.edu
```

Obviously, you'll need to replace `russfeld` with your own username.

If this is the first time you are connecting to a particular server, you'll receive an error message similar to the following:

> The authenticity of host 'cislinux.cs.ksu.edu (129.130.10.43)' can't be established.  
> ECDSA key fingerprint is SHA256: \<random_text\>.  
> Are you sure you want to continue connecting (yes/no)?


As a security feature, the SSH client will remember the identity of each server you connect to using this fingerprint. Since this is the first time you have connected to this server, it doesn't have a fingerprint stored, and it will ask you to confirm that the one presented is correct. If you wanted to, you could contact the owner of the server and ask them to verify that the fingerprint is correct before connecting, but in practice that is usually not necessary. However, once you've accepted the fingerprint, it will store it and check the stored fingerprint against the one presented on all future connections to that server.

If, at any point in the future, the fingerprints don't match, you will be presented with a similar error message. In that case, however, you should be very cautious. It could be the case that the server was recently reset by its owner, in which case you can easily contact them to verify that fact. However, it could also be the case that someone is attempting to either listen to your connection or have you connect to a malicious server. In that case, you should terminate the connection immediately, or else they could possibly steal your credentials or worse.

In any case, since this is our first time connecting, just type `yes` to store the fingerprint and continue connecting. You'll then be asked to provide your password. Note that when you enter your password here it will not show any indication that you are entering text, so you must type carefully. If the password is accepted, you'll be given access to the system.

On that system, you can run any command that you normally would. You can even run graphical programs remotely via SSH, but that requires a bit more configuration and software which I won't go into here. Once you are finished, you can type `exit` to close the remote session and return to your own computer.

Next, let's discuss the SSH server. It is available as open-source software for Linux, and can easily be installed on any system running Ubuntu Linux using the `apt` command:

```bash
sudo apt install openssh-server
```

Once it has been installed, you can verify that it is working by using the `ssh` command to connect to your own system:

```bash
ssh localhost
```

If this is the first time you have done so, you should get the usual warning regarding host authenticity. You can simply type `yes` to continue connecting, then provide your password to log on to the system. Once you have verified that it is working, type `exit` to return to the local terminal. If your server is connected to a network, you can use `ssh` to connect to it just like you would any other server. Note that you may have to configure your firewall to allow incoming SSH connections, typically on port 22.

The SSH server has many options that you can configure. You can edit the configuration file using this command:

```bash
sudo nano /etc/ssh/sshd_config
```

There are many great resources online to help you understand this file. In general you can use the default settings without any problems, but there are a couple of lines you may want to change. Note that any line prefixed with a hash symbol `#` is a code comment, so you will need to remove that symbol for the change to be read. The commented lines reflect the default settings, which can be overridden by un-commenting the line and changing the value.

The first line you may want to change is:

```bash
#Port 22
```

This line defines the port that SSH listens on. By default, SSH uses port 22, a well-known port for that service. However, since everyone knows that SSH uses port 22, it is very common for servers connected to the internet to receive thousands of malicious login attempts via that port in an attempt to discover weak passwords and usernames. By changing the SSH port to a different port, you can eliminate much of that traffic. Of course, if you change this port here, you may also need to update your firewall rules to allow the new port through the firewall.

The other line worth looking at is:

```bash
#PasswordAuthentication yes
```

By changing this line to `no` you can require that all users on your system use SSH keys to log in, which are generally much more secure than passwords. We'll discuss SSH keys shortly. Remember to make sure your own SSH key is properly configured before changing this setting, or you may lock yourself out from your own system.

If you make any changes to the configuration file, you can restart the server using the following command:

```bash
sudo systemctl restart ssh
```

You can also always check the status of the server using this command:

```bash
sudo systemctl status ssh
```

To make your life a bit easier, let's discuss SSH keys. Instead of providing a password each time you want to log on to a system with SSH, you can have your computer automatically provide a key to prove your identity. Not only is this simpler for you, but in many cases it is much more secure overall.

To use SSH keys, you must first generate one. You'll need to perform this step on the computer you plan to connect from, not on the server you'll connect to. In Terminal, type the following command to start the process:

```bash
ssh-keygen -t rsa -b 4096
```

This will generate a public & private RSA keypair with a 4096 bit size, generally regarded as a very secure key by most standards.

The command will first ask you where to store the key. It defaults to `~/.ssh/id_rsa` which is the standard location, so just press enter to accept the default.

Next, it will ask you to set a passphrase for your key. If you are setting up the key on a secure computer that only you would have access to, you can leave this blank to not set a passphrase on the key. In that way, you won't have to enter any passwords to use SSH with this key. However, if anyone gains access to the key file itself, they can easily log in to any system as you with that key until you revoke access. If you want your keys to be more secure, you can set a passphrase to lock the key. The downside is that you'll have to provide the passphrase for the key in order to use it, but it is still more secure than providing the password to the user account itself.

Once the key is created, it will give you some information about where it is stored. You can view those files by typing the following:

```bash
ls ~/.ssh/
```

There should be at least two files here. The first, `id_rsa`, is your private key. Do not share that file with anyone! You may choose to make a backup of that file for your own use, if desired. However, if the key was not protected with a passphrase when it was created, you should protect that file as closely as if it contained all of your passwords in plain text.

The second file, `id_rsa.pub`, is your public key. This is the file we'll need to give to other servers so that we can log on using our private key. There are a couple of ways to do so. First, I'll show you the automatic way, then I'll discuss what it does so you could do it manually if needed.

To send your public key to a remote server, we'll use the `ssh-copy-id` command. Its syntax is very similar to the normal SSH command. For example, to send my new public key to the CS Linux server, I would do the following:

```bash
ssh-copy-id russfeld@cslinux.cs.ksu.edu
```

It will prompt you for your password, and if it succeeds it will install the key on that server. You can then verify that it worked by using the normal SSH command to connect. It should succeed without asking you to provide any password, except possibly the passphrase for your SSH key.

Once on that server, we can see where the key gets installed. It is usually placed in a file at `~/.ssh/authorized_keys`. On some systems, it may be `~/.ssh/authorized_keys2` due to a security vulnerability, or both files may be present. This is configurable in the SSH Server configuration file.

In that `authorized_keys` file, you'll see a copy of your public key on a single line. To add additional keys to the system, you can either use the `ssh-copy-id` command from the system containing the new key, or copy and paste the public keys directly into this file, one per line. To remove a key, simply delete the corresponding line from this file. Note that at the end of the line you can see the username and computer name from the machine where the key was created, which can be very helpful in identifying keys.

Finally, there is one other trick you can use to make working with SSH servers much more useful, and that is through the use of an SSH config file. First, make sure you are back on your local computer and not on any remote servers. Check the command prompt carefully, or type `exit` a few times to make sure you have closed all SSH sessions. On your local computer, open a new SSH config file using the following command:

```bash
nano ~/.ssh/config
```

By convention, your SSH config file should reside in that location. In that file, you can configure a wide variety of host settings for the servers you connect to. For example, here is one entry from my own SSH config file:

```bash
Host cs
    HostName cslinux.cs.ksu.edu
    Port 22
    User russfeld
    IdentityFile ~/.ssh/id_rsa
```

The first line gives the short name for the host. Then, all lines below it give configuration information for that host. For example, here I've given the hostname (you can also use an IP address), the port, the username, and the private key file that should be used when connecting to this host. These are all options that you'd normally have to provide on the command line when using the `ssh` command. By placing them here, you can just reference the host by its short name, and all of this information will automatically be used when you connect to that system.

With this in place, all I have to do to connect to the CS Linux servers is type:

```bash
ssh cs
```

and all my other options are read from this configuration file. Pretty nifty, right?

There are many other options you can include in your SSH config file. I recommend checking out the links in the resources section for more information.

I hope this video will be very useful to you as you work with SSH throughout this semester and in the future. I know much of this information has been very helpful to me in my career thus far.
