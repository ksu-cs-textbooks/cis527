---
title: "DevOps"
weight: 10
pre: "2. "
---

{{< youtube xluKa4AyUNE >}}

#### Resources

* **[Slides]({{< relref "/7-backups-monitoring-devops/02-devops-slides.md" >}})**
* **[Extras - Git]({{< relref "/X-extras/07-git" >}})**
* [DevOps](https://en.wikipedia.org/wiki/DevOps) on Wikipedia
* [Infrastructure as Code](https://en.wikipedia.org/wiki/Infrastructure_as_Code) on Wikipedia
* [What is DevOps?](https://aws.amazon.com/devops/what-is-devops/) from Amazon Web Services
* [What Is DevOps?](https://theagileadmin.com/what-is-devops/) from The Agile Admin
* [DevOps: Breaking the Development-Operations Barrier](https://www.atlassian.com/devops) from Atlassian
* [Periodic Table of DevOps Tools](https://xebialabs.com/periodic-table-of-devops-tools/) from XebiaLabs
* [The Ultimate DevOps Tool Chest](https://xebialabs.com/the-ultimate-devops-tool-chest/) from XebiaLabs
* [webhook](https://github.com/adnanh/webhook) on GitHub
* [webhook Hook Examples](https://github.com/adnanh/webhook/blob/master/docs/Hook-Examples.md) on GitHub
* [Webhooks](https://docs.gitlab.com/ee/user/project/integrations/webhooks.html) on GitLab Documentation

#### Video Transcript

One of the hottest new terms in system administration and software development today is DevOps. DevOps is a shortened form of "Development Operations," and encompasses many different ideas and techniques in a single term. I like to think of it as the application of the Agile software development process to system engineering. Just as software developers are focusing on more frequent releases and flexible processes, system administrators have to react to quickly changing needs and environments. In addition, DevOps engineers are responsible for automating much of the software development lifecycle, allowing developers to spend more time coding and less time running builds and tests manually. Finally, to accommodate many of these changes, DevOps engineers have increasingly adapted the concept of "infrastructure as code," allowing them to define their system configurations and more using tools such as Puppet and Ansible in lieu of doing it manually. As we saw in Module 2, that approach can be quite powerful.

Another way to think of DevOps is the intersection of software development, quality assurance, and operations management. A DevOps engineer would work fluidly with all three of these areas, helping to automate their processes and integrate them tightly together.

There are many different ways to look at the DevOps toolchain. This graphic gives one, which goes through a process of "plan, create, verify, package, release, configure, and monitor." The first four steps deal with the development process, as developers work to plan, test, and package their code for release. Then, the operations side takes over, as the engineers work to make that code widely available in the real world, dealing with issues related to configuration and monitoring.

For this lecture, I'll look at a slightly modified process, consisting of these seven steps. Let's take a look at each one in turn and discuss some of the concepts and tools related to each one.

First is code. As software developers work to create the code for a project, DevOps engineers will be configuring many of the tools that they use. This could be managing a GitHub repository, or even your own GitLab instance. In addition, you could be involved in configuring their development and test environments using tools such as Vagrant and Puppet, among others. Basically, at this phase, the responsibility of a DevOps engineer is to allow developers to focus solely on creating code, without much worry about setting up the environments and tools needed to do their work.

The next steps, build and test, are some of the most critical for this process. As developers create their code, they should also be writing automated unit tests that can be run to verify that the code works properly. This is especially important later on, as bugfixes may inadvertently break code that was previously working. With a properly developed suite of tests, such problems can easily be detected. For a DevOps engineer, the most important part is automating this process, so that each piece of code is properly tested and verified before it is used. Generally, this involves setting up automated building and testing procedures using tools such as Travis and Jenkins. When code is pushed to a Git repository, these tools can automatically download the latest code, perform the build process, and run any automated tests without any user intervention. If the tests fail, they can automatically report that failure back to the developer.

Once the product is ready for release, the package and release processes begin. Again, this process can be fully automated, using tools in the cloud such as Heroku, AWS, and Azure to make the software available to the world. In addition, there are a variety of tools that can be used to make downloadable packages of the software automatically. For web-based applications, this process could even be chained directly after the test process, so that any build that passes the tests is automatically released to production.

Of course, to make a package available in production requires creating an environment to host it from, and there are many automated configuration tools to help with that. We've already covered Puppet in this class, and Ansible and SaltStack can perform similar functions in the cloud. In addition, you may choose to use container tools such as Docker to make lightweight containers available, making deployment across a variety of systems quick and painless.

Lastly, once your software is widely available, you'll want to continuously monitor it to make sure it is available and free of errors. There are many free and paid tools for performing this task, including Nagios, Zabbix, and Munin. As part of this lab's assignment, you'll get to set up one of these monitoring tools on your own cloud infrastructure, just to see how they work in practice.

Of course, one of the major questions to ask is "Why go to all this trouble?" There are many reasons to consider adopting DevOps practices in any organization. First and foremost is to support a faster release cycle. Once those processes are automated, it becomes much easier to quickly build, test, and ship code. In addition, the whole process can be more flexible, as it is very easy to change a setting in the automation process to adapt to new needs. This supports one of the core tenets of the agile lifecycle, which focuses on working software and responding to change. In addition, DevOps allows you to take advantage of the latest developments in automation and virtualization, helping your organization stay on top of the quickly changing technology landscape. Finally, in order for your environment to be fluidly scalable, you'll need to have a robust automation architecture, allowing you to provision resources without any human interaction. By adopting DevOps principles, you'll be ready to make that leap as well.

Finally, to give you some experience working with DevOps, let's do a quick example. I've named this the "Hello World" of DevOps, as I feel it is a very good first step into that world, hopefully opening your eyes to what is possible. You'll perform this activity as part of the assignment for this lab as well.

First, you'll need to create a project on the K-State CS GitLab server, and push your first commit to it. You can refer to the Git video in the Extras module for an overview of that process. I'm going to use an existing project, which is actually the source project for this course. We'll be using the Webhooks feature of this server. When certain events happen in this project, we can configure the server to send a web request to a particular URL with the relevant data. We can then create a server to listen for those requests and act upon them.

You will also need to either configure SSH keys for your GitLab repository, or configure the repository to allow public access.

Next, we'll need to install and configure the `webhook` server on our DigitalOcean droplet. It is a simple server that allows you to listen for those incoming webhooks from GitHub and GitLab, and then run a script when they are received. Of course, in practice, many times you'll be responsible for writing this particular piece yourself in your own environment, but this is a good example of what it might look like.

On my Ubuntu cloud server, I can install `webhook` using APT:

```bash
sudo apt update
sudo apt install webhook
```

Next, I'll need to create a file at `/etc/webhook.conf` and add the content needed to create the hook:

```json
[
  {
    "id": "cis527online",
    "execute-command": "/home/cis527/bin/cis527online.sh",
    "command-working-directory": "/var/www/bar/html/",
    "response-message": "Executing checkout script",
    "trigger-rule":
    {
      "match":
      {
        "type": "value",
        "value": "f0e1d2c3b4",
        "parameter":
        {
          "source": "header",
          "name": "X-Gitlab-Token"
        }
      }
    }
  }
]
```

You can find instructions and sample hook definitions on the `webhook` documentation linked in the resources section below this video. You'll need to configure this file to match your environment. Also, you can use this file to filter the types of events that trigger the action. For example, you can look for pushes to specific branches or tags.

Since this file defines a script to execute when the Webhook is received, I'll need to create that script as well:

```bash
#!/bin/bash

git pull
exit 0
```

This script is a simple script that uses the `git pull` command to get the latest updates from Git. I could also place additional commands here if needed for this project.

Once I create the script, I'll need to modify the permissions to make sure it is executable by all users on the system:

```bash
chmod a+x bin/cis527online.sh
```

Once everything is configured, I can restart the `webhook` server using this command:

```bash
sudo systemctl restart webhook
```

Then, if everything is working correctly, I can test it using my cloud server's external IP address on port 9000, with the correct path for my hook. For the one I created above, I would visit `http://<ip_address>:9000/hooks/cis527online`. You should see the response `Hook rules were not satisfied` displayed. If so, your `webhook` server is up and running. Of course, you may need to modify your firewall configuration to allow that port.

Lastly, if my repository requires SSH keys, I'll need to copy the public and private keys into the root user's `.ssh` folder, which can be found at `/root/.ssh/`. Since `webhook` runs as a service, the Git commands will be run as that user, and it'll need access to that key to log in to the repo. There are more advanced ways of doing this, but this is one way that works.

I'll also need to download a copy of the files from my Git repository onto this system in the folder I specified in `webhook.conf`

```bash
sudo rm /var/www/bar/html/*
sudo git checkout <repository_url> /var/www/bar/html
```

Now, we can go back to the K-State CS GitLab server and configure our webhook. After you've opened the project, navigate to **Settings** and then **Integrations** in the menu on the left. There, you can enter the URL for your webhook, which we tested above. You'll also need to provide the token you set in the `webhook.conf` file. Under the **Trigger** heading, I'm going to checkmark the "Push events" option so that all push events to the server will trigger this webhook. In addition, I'll uncheck the option for "Enable SSL verification" since we have not configured an SSL certificate for our `webhook` server. Finally, I'll click **Add webhook** to create it.

Once it is created, you'll see a **Test** button below the list of existing webhooks. So, we can choose that option, and Select "Push events" to test the webhook. If all works correctly, it should give us a message stating that the hook executed successfully.

However, the real test is to make a change to the repository, then commit and push that change. Once you do, it should automatically cause the webhook to fire, and within a few seconds you should see the change on your server. I encourage you to test this process for yourself to make sure it is working correctly.

There you go! That should give you a very basic idea of some of the tools and techniques available in the DevOps world. It is a quickly growing field, and it is very useful for both developers and system administrators to understand these concepts. If you are interested in learning more, I encourage you to read some of the materials linked in the resources section below this video, or explore some of the larger projects hosted on GitHub to see what they are doing to automate their processes.
