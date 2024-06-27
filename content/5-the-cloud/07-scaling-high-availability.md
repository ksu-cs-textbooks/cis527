---
title: "Scaling & High Availability"
weight: 35
pre: "7. "
---

{{< youtube bYYt0SxQ7MY >}}

<!-- tzgMTxh24pY -->

#### Resources

* **[Slides]({{% relref "/5-the-cloud/07-scaling-high-availability-slides.md"  %}})**
* [An Introduction to Droplet Metadata](https://www.digitalocean.com/docs/droplets/resources/metadata/) from DigitalOcean
* [How to Resize Droplets](https://www.digitalocean.com/docs/droplets/how-to/resize/) from DigitalOcean
* [How to Automate the Scaling of Your Web Application on DigitalOcean Ubuntu 16.04 Droplets](https://www.digitalocean.com/community/tutorials/how-to-automate-the-scaling-of-your-web-application-on-digitalocean-1604) from DigitalOcean
* [Load Balancers](https://www.digitalocean.com/docs/networking/load-balancers/) from DigitalOcean
* [What is High Availability?](https://www.digitalocean.com/community/tutorials/what-is-high-availability) from DigitalOcean
* [AWS Auto Scaling](https://aws.amazon.com/autoscaling/) from Amazon Web Services
* Netflix Case Study
  * [Netflix: What Happens When You Press Play?](http://highscalability.com/blog/2017/12/11/netflix-what-happens-when-you-press-play.html) from High Scalability Blog
  * [Scryer: Netflix's Predictive Auto Scaling Engine](https://medium.com/netflix-techblog/scryer-netflixs-predictive-auto-scaling-engine-a3f8fc922270) from Netflix Technology Blog
  * [Completing the Cloud Migration](https://media.netflix.com/en/company-blog/completing-the-netflix-cloud-migration) from Netflix
  * [DevOps Case Study: Netflix and the Chaos Monkey](https://insights.sei.cmu.edu/devops/2015/04/devops-case-study-netflix-and-the-chaos-monkey.html) from DevOps Blog at CMU Software Engineering Institute
  * [Chaos Engineering Upgraded](https://medium.com/netflix-techblog/chaos-engineering-upgraded-878d341f15fa) from Netflix Technology Blog

#### Video Transcript

One of the major selling points of the cloud is its rapid elasticity, or the ability of your cloud resources to grow and shrink as needed to handle your workload. In this video, you'll learn a bit more about how to configure your cloud resources to be elastic, as well as some of the many design decisions and tradeoffs you'll face when building a cloud system.

First, let's talk a bit about scalability. If you have a cloud system, and find that it does not have enough resources to handle your workloads, there are generally two ways you can solve that problem. The first is to scale vertically, which involves adding more CPU and RAM resources to your cloud systems. Effectively, you are getting a bigger, more powerful computer to perform your work. The other option is to scale horizontally by configuring additional cloud systems to increase the number of resources you have available. In this instance, you are just adding more computers to your organization. In many cases, your decision of which way to grow may depend on the type of work you are performing as well as the performance limitations of the hardware. If you are dealing with a large number of website users, you may want to scale horizontally so you have more web servers available. If you are performing large calculations or working with big databases, it may be easier to scale vertically in order to keep everything together on the same system.

In the case of DigitalOcean, you can scale both horizontally and vertically with ease. To scale horizontally, you'll simply add more droplets to your cloud infrastructure. You may also need to add additional items such as a load balancer to route incoming traffic across multiple droplets. For vertical scaling, you can easily resize your droplets via the DigitalOcean control panel or their API. Unfortunately, to resize a droplet it will need to be rebooted, so you'll have to deal with a bit of downtime unless you have some existing infrastructure for high availability. We'll discuss that a bit later in this video.

Unfortunately, DigitalOcean does not support any automated scaling features at this time. However, they do offer a tutorial online for how to build your own scripts to monitor your droplet usages and provision additional droplets if you'd like to scale horizontally. This diagram shows what such a setup might look like. It has a frontend resource with a load balancer as well as a script to manage scaling, and a number of backend web servers to handle the incoming requests. If you are interested in learning about scaling in DigitalOcean, I encourage you to check out the tutorial linked in the resources section below the video.

One major feature that sets Amazon Web Services apart from DigitalOcean is the ability to perform automatic scaling of AWS instances. Through their control panel, it is very simple to set up a scaling plan to optimize your use of AWS resources to match your particular needs in the cloud. Since AWS is primarily targeted at large enterprise customers, it has many of these features available to help them manage large workloads in the cloud. I've also linked to information about Auto Scaling in AWS in the resources section below the video if you'd like to learn more.

Finally, beyond scaling, you should also consider how to design your systems for high availability when dealing with the cloud. In many organizations, your overall goal is to make your cloud resources available all of the time, without any noticeable errors or downtime. To do that, however, requires quite a bit of planning and an advanced architecture to make it all work properly. Here is a simple example setup from DigitalOcean, showing how you can use six cloud resources to build a simple, highly available system.

First, there are two load balancers. One is acting as the primary, and is assigned to a floating IP address. The secondary load balancer has a connection to the primary, allowing it to monitor the health of the system. If the secondary load balancer detects an error with the primary, it will switch the floating IP to point to itself to handle incoming requests. This change can happen almost automatically, so the users will not experience much downtime at all. Behind the load balancer is two application servers. The load balancers can forward requests to either application server, but they will, of course, detect if one server is down and route all requests to the other server instead. Finally, each application server is attached to a backend database server, each of which are replicated from the other to maintain data consistency. With this setup, as long as both systems of the same type don't fail at the same time, the application should always be available to the users.

---

In the updated assignment for Lab 5, you are asked to create a load balancer between your DigitalOcean droplets to split HTTP traffic between the frontend and backend droplets. Once that is properly set up and configured, you should be able to visit the IP address of the load balancer and see the homepage of one of the two droplets. Then, if you constantly refresh that page, it should swap between the two servers as shown here.

Unfortunately, due to the way we have configured other parts of this lab, it is prohibitively difficult to configure this load balancer to properly handle HTTPS traffic. This is mainly because we are using an external registrar for our domain name so that DigitalOcean cannot manage the domain, and the certificates we are getting from certbot are tied to the actual domain name and not a wildcard. In a production system, we would probably change one of these two things to allow us to send properly secured HTTPS traffic through the load balancer. But, for now, we won't worry about that. 

---

To put it all together, let's look at a quick case study for how to build an effective computing architecture in the cloud. Netflix is one of the pioneers in this area, and arguably has one of the most advanced and robust cloud infrastructures on the internet today.

As you know, Netflix has grown by leaps and bounds over the past decade. This graph shows their total monthly streaming video hours from 2008 through 2015. Since that time, it has continued to grow at an even faster rate. In fact, today Netflix is the platform of choice for viewing TV content among most Americans, beating out basic cable and broadcast TV. As Netflix moved into the streaming video arena, they suffered a few major setbacks and outages in their data centers in 2008, prompting them to move to the cloud. As of January 2016, their service is hosted entirely from the cloud, primarily through Amazon Web Services and their own content delivery network, named Netflix Open Connect.

Of course, moving to the cloud brings its own challenges. This graph shows the daily traffic for five days across Netflix's systems. As you can see, the traffic varies widely throughout the day, peaking and then quickly dropping. To handle this level of traffic, Netflix has a couple of options. They could, of course, scale their system to handle the highest peaks of traffic, and let it set idle during the dips. However, since the cloud should be very elastic, that is a very inefficient use of resources and could end up costing the company a fortune.

In addition, since the traffic peaks and dips so quickly, a reactive scaling approach may not work. According to their technology blog, it can take up to 45 minutes to provision a new cloud resource in their infrastructure, so by the time it is ready to go the traffic may have increased even more. In short, they'd never be able to catch up.

So, Netflix developed Scryer, a predictive scaling tool for their cloud infrastructure. Scryer analyzes traffic patterns and builds a prediction of what the traffic will be in the future, allowing Netflix to proactively scale their resources up before the increase in traffic happens, allowing them to instantly be available when they are needed.

This graph shows the workload predicted by Scryer for a single day as well as the scaling plan that came from that prediction. Netflix has used this to not only improve their performance, but reduce the costs as well.

Of course, scaling is just one piece of the puzzle when it comes to handling large cloud workloads. Many large websites employ high levels of caching, as well as the use of a content distribution network, to lessen the load on their actual cloud infrastructures and reduce the need for scaling. In the case of a content distribution network, or CDN, those websites store their data closer to the users, sometimes directly in the datacenters of internet service providers across the globe. Netflix is no different, and in many cases Netflix has stored content representing 80% or more of its workload directly in the networks of local ISPs. So, while Netflix has all of the data stored on their cloud systems, those systems are usually more involved in sending data to the local content distribution centers than actual individual users.

Finally, Netflix was a pioneer in the area of chaos engineering, or building their systems to expect failure. As they moved into the cloud, they developed tools such as "Chaos Monkey," "Latency Monkey," and even "Chaos Gorilla," all part of their "Simian Army" project, to wreak havoc on their systems. Each of those tools would randomly cause issues with their actual production cloud systems, including shutting down a node, introducing artificial latency, or, in the case of Chaos Gorilla, even cutting off an entire zone. By doing so, Netflix essentially forced itself to build systems that were highly tolerant of failures, to the point that consumers wouldn't even notice if an entire zone went offline.

In fact, these graphs show just such an event, as simulated by Chaos Gorilla. The top shows global traffic, while the bottom shows traffic during the same time period for both the eastern and western US zones. During the test, traffic to the western zone was blocked, resulting in a large amount of traffic being rerouted to the eastern zone. Looking at the graphs, you can clearly see the switchover in the smaller graphs below, but the global graph stayed steady, meaning that users worldwide wouldn't have even noticed a blip in service.

While this may be an extreme example of planning for failures, it goes to show the depth to which Netflix has designed their cloud infrastructure to be both highly scalable to handle fluctuating demand, and highly available to mitigate failures and outages. I've included a whole section of related reading for this Netflix case study in the resources section below the video if you'd like to know more about these topics.

So, as you move forward and continue designing systems for the cloud, here are a few design considerations I feel that you should think about. First, do you plan on scaling out, or scaling up? In addition, is it better to scale predictively, or reactively. Also, does your system need to be designed for high availability, or is it better to save money and simplify the design at the expense of having a bit of downtime once in a while? Finally, no matter what design you choose, you should always be planning for the inevitable failures and outages, and testing any failover procedures you have in case they do happen. Just like the fire drills you might remember from school, it's much better to practice for emergency situations that never happen than to have to deal with an emergency you haven't prepared for in the first place.

That's all for Module 5! In Module 6, you'll continue building both cloud systems as well as enterprise networks as we deal with application servers. In the meantime, you should have everything you need to complete Lab 5. As always, if you have any questions, feel free to post in the course discussion forums to get help. Good luck!
