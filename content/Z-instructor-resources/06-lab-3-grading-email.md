---
title: "Lab 3 Grading Email"
weight: 30
pre: "3.2 "
---

#### Greetings!

Here is the information you'll need to know to get your lab graded.

1. **Grading Date/Time:** \<time\> <br> Contact me ASAP if that time will not work for you for any reason and I will work with you to reschedule.
1. **Zoom Link:** \<link\> <br> If you haven't used Zoom before, I recommend going to https://ksu.zoom.us/ first to download the Zoom client software. Then, when the time comes, click the link above to join the Zoom session.
1. **Your Setup:** <br> Before you join the Zoom session for grading, please have the following steps completed on your end. This helps things go as smoothly as possible:
  1. Use the fastest internet connection available to you. If you are using a laptop with a wireless connection, you may want to plug in to a hard-wired connection if available. If you can work from campus, that may be best, depending on your home internet connection.
  1. Make sure your audio input device (microphone) is working in Zoom. You are not required to have a webcam, but you are welcome to use one if you like. I will be using a webcam and microphone on my end.
  1. Confirm that all the VMs for this lab are booted and running on your system.
  1. We'll be using the desktop sharing features of Zoom so I can see your VMs. So, make sure you close any windows or programs that are running in the background that shouldn't be shared with me.
1. **Operations:** <br>Here are a few operations you may be asked to demonstrate:
  1. Connect remotely to Ubuntu via SSH
  1. Connect remotely to Windows via Remote Desktop
  1. Show Static IP Address Settings in Ubuntu
  1. DNS server settings: `/etc/bind/named.conf.options`, `/etc/bind/named.conf.local` and related zone files
  1. DNS server lookup test: `dig ubuntu.cis527<your eID>.cs.ksu.edu` or `nslookup ubuntu.cis527<your eID>.cs.ksu.edu`
  1. DNS server reverse test: `dig -x xxx.xxx.xxx.41` or `nslookup xxx.xxx.xxx.41`
  1. DHCP server settings: `/etc/dhcp/dhcpd.conf`
  1. DHCP server test: `ipconfig /release` and `ipconfig /renew` from Windows
  1. SNMP server test: `snmp` demonstration from Ubuntu Client
  1. SNMP screenshots (3)
  1. Wireshark screenshots (8)
1. **Finality** <br> Once you begin the grading process, no changes may be made to your system to fix any errors encountered. The grade you receive will reflect the state of your VMs at the start of the grading process. This is to ensure that grades are fairly determined and that no special consideration is given.

That should cover everything. Please let me know if you have any questions prior to your scheduled grading time.

_Good luck!_<br>
Russ
