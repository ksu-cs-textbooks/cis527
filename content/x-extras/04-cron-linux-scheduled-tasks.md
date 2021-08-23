---
title: "Cron (Linux Scheduled Tasks)"
weight: 20
pre: "4. "
---

{{< youtube OJNPy47YYok >}}

#### Resources

* [Cron How To](https://help.ubuntu.com/community/CronHowto) from Ubuntu
* [Linux Cron Guide](https://linuxconfig.org/linux-cron-guide) from LinuxConfig.org

#### Video Transcript

This video introduces the Cron tool on Linux, which can be used to run tasks automatically at specific times on your system. It is a very handy piece of software, but a little confusing at first.

To view the current list of scheduled tasks for your user, use the following command:

```bash
crontab -l
```

Generally, you probably won't see anything there at first. You can also view the list for the root user using the `sudo` command

```bash
sudo crontab -l
```

Depending on the software installed on your system, you may already see a few entries there.

To edit the schedule, use the same command with a `-e` option:

```bash
crontab -e
```

It should open the file with your default text editor, usually Nano. At the top of the file, it gives some information about how the file is constructed. At the bottom, you can add lines for each command you'd like to run. There are 6 columns present in the file, in the following order:

1. `m` - minute (0-59)
1. `h` - hour (0-23)
1. `dom` - day of month (1-31)
1. `mon` - month (1-12)
1. `dow` - day of week (0=Sunday, 1=Monday, ... 7=Sunday)
1. `command` - full path to the command to be run, followed by any parameters

The [Linux Cron Guide](https://linuxconfig.org/linux-cron-guide) from LinuxConfig.org has a great graphic describing these columns as well. All you have to do is add your entries and save the file, and the new settings will be applied automatically.

Honestly, the best way to learn cron is by example. For example, assume we have a script at `/home/cis527/bin/script.sh` that we'd like to run. If we add the following entry:

```
15 5 * * * /home/cis527/bin/script.sh
```

it will run the script at 5:15 AM every day. Note that the amount of whitespace between each column doesn't matter; it will treat any continuous sequence of spaces and tabs as a single whitespace, much like HTML. So, feel free to align your columns however you choose, as long as they are in the correct order and separated by at least one whitespace character.

Let's look at some other examples:

```
0 */6 * * * /home/cis527/bin/script.sh
```

This will run the script every six hours (note the `*/6`, meaning that every time the hour is divisible by 6, it will run the script). So, it will run at 12 AM, 6 AM, 12 PM, and 6 PM each day.

```
10,30,50 * 15 * 5 /home/cis527/bin/script.sh
```

This will run every hour at 10, 30 and 50 minutes past the hour, but only on the 15th day of each month and every Friday. Note that the day of week option is generally separate from the day of month option. If both are included, it will run on each indicated day of the week, as well as the indicated day of the month.

```
0 5 * * 1-5 /home/cis527/bin/script.sh
```

This will run at 5:00 AM each weekday (Monday=1 through Friday=5)

```
@reboot /home/cis527/bin/script.sh
```
This will run once each time the system starts up.

There are many, many more ways to use cron, but hopefully this video gives you enough information to get started. Good luck!
