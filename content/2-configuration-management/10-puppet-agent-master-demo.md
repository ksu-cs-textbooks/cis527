---
title: "Puppet Agent & Master Demo"
weight: 50
pre: "10. "
---

{{% notice info "Puppet Learning VM Deprecated" %}}

_As of 2023, the Puppet Learning VM is no longer being maintained. The videos below demonstrate some of the features of Puppet, which can also be done on your Ubuntu VM after installing Puppet Agent. Unfortunately, it is not easily possible to simulate an enterprise Puppet setup without this VM, so I'll keep these videos up for demonstration purposes._ --Russ

{{% /notice %}}

{{< youtube M84N1TbRB-g >}}

#### Resources

* [Overview of Puppet's Architecture](https://puppet.com/docs/puppet/latest/architecture.html) from Puppet

#### Video Script

In this video, I'll give a quick demonstration of what a true enterprise Puppet setup might look like. Once again, I'm going to be using the Learning Puppet VM, and this time I'll be following the `agent_run` quest to demonstrate these features.

The `agent_run` quest gives us a client system already set up and ready to go. We can access it using SSH:

```bash
ssh learning@agent.puppet.vm
```

Once we are on that system, we can try to force a Puppet Agent run using the following command:

```bash
sudo puppet agent -t
```

However, when the Puppet Agent tries to contact the Puppet Master server, it presents an error about client certificates. As a security measure, we must sign the certificate for each agent that tries to contact the server before it will be allowed access. Without this step, any malicious user could gain valuable information about our system configuration by talking with the Puppet Master.

To sign that certificate, we can go back to the Puppet Master by exiting the current SSH session:

```bash
exit
```

Then we can use this command to show all the unsigned certificates on the system:

```bash
sudo puppet cert list
```

To sign a certificate, we can use this command:

```bash
sudo puppet cert sign agent.puppet.vm
```

Now, we can reconnect to our agent node:

```bash
ssh learning@agent.puppet.vm
```

And try to run the agent again:

```bash
sudo puppet agent -t
```

This time, we should be successful. However, we haven't really told Puppet what we want configured on this system. So, let's go back to the Puppet Master and do so:

```bash
exit
```

On the Puppet Master, we would like to edit the manifest file used to configure each system. As before, I'll quickly install Nano to make editing files much simpler, but feel free to use Vim if you would like:

```bash
sudo yum install nano
```

Next, we'll edit the default site manifest file, which is located at the end of a very long directory path:

```bash
nano /etc/puppetlabs/code/environments/production/manifests/site.pp
```

This is the default site manifest file for this system. On an actual system, you may define different environments and roles for each system, which may alter the path to this file. For this example, we'll just make a quick edit to show how it can be done.

At the bottom of the file, add the following:

```pp
node 'agent.puppet.vm' {
  notify { "Hello Puppet!": }
}
```

Then, use <kbd>CTRL</kbd>+<kbd>X</kbd>, then <kbd>Y</kbd>, then <kbd>ENTER</kbd> to save and close the file.

Finally, return to the agent VM:

```bash
ssh learning@agent.puppet.vm
```

and run Puppet Agent once again:

```bash
sudo puppet agent -t
```

If done correctly, you should see a notification of `"Hello Puppet!"` in the output.

This is a very short demo of the power of Puppet's Master and Agent architecture. The Puppet Learning VM quests go much more in-depth in ways to use Puppet in an organization. I highly encourage you to review that information if you are interested, but it is not required to complete Lab 2.
