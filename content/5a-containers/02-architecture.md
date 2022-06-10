---
title: "Architecture"
weight: 10
pre: "2. "
---

{{< youtube >}}

#### Resources

* **[Slides]({{< relref "./02-architecture-slides.md" >}})**
* **[Docker Tutorial for Beginners](https://www.youtube.com/watch?v=3c-iBn73dDE)** by TechWorld with Nana on YouTube
* [Docker Overivew](https://docs.docker.com/get-started/overview/) from Docker
* [Container Report](https://www.datadoghq.com/container-report/) from Datadog
* [GitHub Codespaces Overview](https://docs.github.com/en/codespaces/overview) from GitHub
* [Virtual Machine-Based Features in Codio](https://www.codio.com/webinar-virtual-machine-based-features-in-codio) from Codio

#### Video Transcript

Up to this point, we've been working with traditional virtual machines in our labs. To use a traditional virtual machine, we first install a hypervisor that allows us to run multiple VMs on a single system. That hypervisor may be installed directly on the hardware, as it is in most enterprise settings, or we may install the hypervisor on top of an existing operating system, like we've done with VMWare on our own computers. Then, inside of the virtual machine, we install another entire operating system, as well as any of the software we need to run our applications. If we want to have multiple VMs that all run the same operating system, we'll have to install a full copy of that operating system in each VM, in addition to the operating system that may be installed outside of our hypervisor. Can you spot a possible problem here?

In traditional VM architectures, we may end up wasting a lot of our time and resources duplicating the functions of an operating system within each of our virtual machines. This can lead to very bloated virtual machines, making them difficult to move between systems. In addition, we have to manage an entire operating system, complete with security updates, configuration, and more, all within each virtual machine. While there are many tools to help us streamline and automate all of this work, in many ways it can seem redundant.

This is where containers come in. Instead of a hypervisor, we install a container engine directly on our host operating system. The container engine creates an interface between the containers and the host operating system, allowing them to share many of the same features, so we don't need to install a full operating system inside of a container. Instead, we just include the few parts we need, such as the basic libraries and command-line tools. Then, we can add our application directly on top of that, and we're good to go. Containers are often many times smaller than a comparable virtual machine, making them much easier to move between systems, or we can just choose to run multiple instances of the same container to provide additional redundancy. In addition, as we'll see later, containers are built from read-only images, so we don't have to worry about any unwanted changes being made to the container itself - a quick restart and we're back to where we started! With all of those advantages, hopefully you can see why containers have quickly become one of the dominant technologies for virtualization in industry today.

---

In this course, we're going to take a deep dive into using Docker to create and manage our containers. Docker is by far the most commonly used container platform, and learning how to work with Docker is quickly becoming a must-have skill for any system administrator, as well as most software developers. So, learning how to use Docker is a great way to build your resume, even if you aren't planning to work in system administration!

---

Docker itself consists of three major parts. First, we have the Docker client, which is either the Docker command-line tool or a graphical interface such as Docker Desktop. We use the client to interface with the rest of the system to create and manage our containers. Behind the scenes, we have the Docker engine, also known as the Docker daemon, which handles actually running our containers as well as managing things such as images, networks, and storage volumes. We'll spend the next several parts of this module exploring the Docker client and engine. Finally, Docker images themselves are stored on a registry such as Docker Hub, allowing us to quickly find and use images for a wide variety of uses. Many code repositories such as GitHub and GitLab also can act as registries for container images, and you can even host your own!

---

Next, let's look at the structure of a typical container. A container is a running instance of an image, so we can think of a container like an _object_ in object-oriented programming, which is instantiated from an image, acting like a _class_ in this example. An image consists of several layers, which are used to build the file system of the image. Each time we make a change to the contents of an image, such as installing a piece of software or a library, we generate a new layer of the image. This allows us to share identical layers between many images! For example, if we have multiple images that are build using the same Ubuntu base image, we only have to store one copy of the layers of the Ubuntu base image, and then each individual image just includes the layers that were added on top of the base image! This makes it easy to store a large number of similar images without taking up much storage space, and we can even take advantage of this structure to cache layers as we build our own images! 

When we create a container from an image, we add a small, temporary read/write layer on top of the image layers. This is what allows us to instantiate the container and have it act like a running system. As soon as we stop the container, we discard the read/write layer, which means that any data added or changed in the container is lost, unless we make arrangements to have it stored elsewhere. So, this helps us maintain a level of confidence that any container started from an image will always be the same, and we can restart a container anytime to revert back to that state. 

---

So, as we saw earlier, we can easily instantiate multiple copies of the same image into separate containers. Each of those containers will have their own read/write layer, but they'll share the same base image. This makes it extremely easy to deploy multiple instances of the same container on a single system, allowing us to quickly build in redundancy and additional capacity quickly. 

We can also use this to build really interesting infrastructures! Consider developer tools such as GitHub Codespaces or educational tools like Codio - behind the scenes, those platforms are simply instantiating containers based on a shared image that contains all of the development tools and information that the user needs, and once the user is done with their work, the container can be either paused to save computing resources, or it can be destroyed if no longer needed by the user. 

---

So, in summary, why should we consider using containers in our infrastructure instead of the virtual machines we've been learning about so far? Well, for starters, we know that images for containers are typically much smaller than traditional virtual machines, and the use of layers and de-duplication allows us to further reduce the storage needed by images that share a common ancestor. In addition, since the image itself is somewhat decoupled from the underlying operating system, it becomes very easy to decouple our applications from the operating system it runs on. We've also discussed how containers and images are very portable and scalable, so it is very easy to start and run a container just about anywhere it is needed. Finally, as we'll see later in this module, there are many tools available to help us orchestrate our containers across many systems, such as Kubernetes. 

One topic we really haven't talked about yet is sandboxing. This is another great feature of containers that really can't be overlooked. Consider a traditional web-hosting scenario, where a single server has a webserver such as Apache installed, as well as a database, email server, and more. Since all of those applications are installed on the same operating system, a vulnerability in any one of them can allow an attacker access to the entire system! Instead, if each of those applications is running in a separate container, we can easily isolate them and control how they communicate with each other, and therefore prevent a vulnerability in one application from affecting the others! Of course, this depends on us properly configuring our container engine itself, and as we'll see later in this lab, it is very easy to unintentionally introduce security concerns unless we truly understand what we are doing. 

---

As we've already heard in this video, containers are quickly becoming one of the most used tools in system administration today. According to Docker, as of April 2021, there have been over 300 billion individual image downloads from Docker Hub, with 10% of those coming just in the last quarter! There are also over 8.3 million individual image repositories hosted on Docker Hub, meaning that nearly any self-hosted piece of software can probably be found on Docker Hub in some form. 

---

Datadog also publishes their list of the top technologies running in Docker among their clients. Looking here, there aren't too many surprises - we see that the Nginx webserver, Redis key-value database, and Postgres relational database are the top three images, with many other enterprise tools and data storage platforms close behind. 

---

Hopefully this gives you a good overview of the architecture of containers and some of the technology behind the scenes. In the next few parts of this lab, we're going to dive directly into using Docker on our own systems.