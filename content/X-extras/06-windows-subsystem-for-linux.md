---
title: "Windows Subsystem for Linux"
weight: 30
pre: "6. "
---

{{< youtube f2biSfCC26Q >}}

#### Resources

* [Windows 10 WSL Installation Guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10) from Microsoft
* [Windows Subsystem for Linux Documentation](https://docs.microsoft.com/en-us/windows/wsl/about) from Microsoft

#### Video Transcript

In this video, I will briefly introduce the Windows Subsystem for Linux, or WSL, which was one of the most highly anticipated features added to Windows 10 in the last couple of years. WSL allows you to install a full Linux distribution right inside your Windows 10 OS, giving you terminal access to some of your favorite Linux programs and tools. You can even run services such as sshd, MySQL, Apache, and more directly in WSL.

First, you must enable the feature on Windows. The simplest way to do this is to open a PowerShell window using the **Run as Administrator** option, then enter the following command:

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

Once it is complete, you will need to reboot your computer to enable to feature.

Once you have rebooted, you can go to the Windows Store and install the distribution of your choice. There are many to choose from, and you can even have multiple distributions installed at the same time. For this example, I'll choose Ubuntu.

Once it has finished installing, you must open it once to complete the initialization. During that process, you'll be asked to create a username and password for your Linux system. It doesn't have to be the same as your Windows user account, and it will not be synchronized with your Windows password either.

As soon as it is complete, you'll be taken to your Linux distribution's shell. Pretty neat, right?

So, what can you do from here? Pretty much anything! Here are a few things I suggest doing right off the bat.

First, you can update your system just like any other Linux system:

```bash
sudo apt update
sudo apt upgrade
```

You can also set up SSH keys so you can use SSH from WSL instead of dealing with PuTTY or other Windows-based terminal programs. Refer to the Extra - SSH page for more information on how to do that.

On WSL, you can find your normal Windows drives at `/mnt` by doing:

```bash
ls /mnt
```

To get easy access to your Windows files, you can add a symbolic link to your Windows user folder, or any folder you choose. For example, if your Windows username is `cis527` you can use the following command to add a shortcut in your Windows home folder within your WSL home folder:

```bash
ln -s /mnt/c/Users/cis527/ ~/cis527
```

You can verify that it worked using this command:

```bash
ls -l
```

I've used this to create a few useful shortcuts to allow me to easily access my Windows files.

Finally, since I am a big fan of using Git on command line, I usually install Git on my WSL to allow me to easily manage my repositories just like I normally do on my Linux based development systems.

I hope you enjoy working with WSL as much as I have. If you have any suggestions of cool uses for WSL that I missed, feel free to send them to me. You just might get some extra credit points and see your idea featured here in a future semester!
