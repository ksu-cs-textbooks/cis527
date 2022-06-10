---
title: "Docker"
weight: 15
pre: "3. "
---

{{< youtube >}}

#### Resources

* **[Slides]({{< relref "./03-docker-slides.md" >}})**
* **[Docker Tutorial for Beginners](https://www.youtube.com/watch?v=3c-iBn73dDE)** by TechWorld with Nana on YouTube
* [Docker Manuals](https://docs.docker.com/desktop/) from Docker
* [Docker Official Images](https://hub.docker.com/search?q=&type=image&image_filter=official) on DockerHub
* [Docker Hello World](https://hub.docker.com/_/hello-world) on DockerHub
* [Docker Nginx](https://hub.docker.com/_/nginx) on DockerHub

#### Video Transcript

Now that we've covered the general architecture of containers, let's dive a bit deeper into Docker itself. Docker is by far the most commonly used tool for creating and managing containers on a small scale, and learning how to use it is a super useful skill for just about any one in a system administration or software development field. So, let's take a look at!

---

First, let's go over some general terminology related to containers. Recall that an **image** is a read-only template that is used to build a container. The image itself consists of several layers, and may be built on top of another existing image. 

When we launch an image, it is instantiated into a **container**. A container is a running instance of an image, and it includes the read/write layer as well as any connections to resources such as networks, volumes, and other tools.

Finally, a **volume** in Docker is a persistent storage location for data outside of a container. We'll explore how to create volumes and store data from a container later in this lab. 

---

Docker itself consists of several different components. The Docker engine, also known as the Docker daemon, is the tool that is installed on the system that will host the containers. It manages creating containers from images and connecting them to various resources on the system. 

The Docker client is the command-line tool that we use to interface with the Docker engine. On systems with a GUI, we can also install Docker Desktop, which acts as a client for interfacing with Docker, but it also includes the Docker engine. In many cases, installing Docker desktop is the best way to get started with Docker on our own systems, but when working in the cloud we'll generally install the traditional Docker engine and client.

Along with the Docker client, we have another tool known as Docker compose. Docker compose allows us to build configuration files that define one or more containers that should work together, and we can also use Docker compose to easily start and stop multiple containers quickly and easily. I generally prefer working with Docker compose instead of the Docker client, but it is really just personal preference. There are also 3rd party tools that can interface with Docker, such as Portainer, that can do much of the same work.

Finally, we also need to know about registries for container images. Docker Hub is by far the most well known of these, but it is also important to know that both GitHub and GitLab can act as a registry for Docker images. Some companies, such as Microsoft, also choose to host their own registries, so many of the .NET Docker images must be downloaded directly from Microsoft's own registry instead of Docker Hub. For this course, we'll just use Docker Hub and the official images hosted there.

---

So, to get started with Docker, there are several commands that we'll end up using. We'll see these put into practice over the next few parts of this lab, so don't worry about memorizing them right now, but I want to briefly review them so you'll know what they are for when you see them used in the later examples.

First, to get an image from an image registry, we use the `docker pull` command. This will download the image and store it locally on your system. To review the images available on your system, you can use the `docker images` commands.

Once we have an image, we can instantiate it into a container using the `docker run` command. Thankfully, `docker run` is also smart enough to download an image if we don't have it locally, so in many cases it is sufficient to simply use `docker run` to both get an image and start a container. 

Once a container is created, we can use `docker stop` and `docker start` to stop and start an existing container. This is helpful if we want to effectively "pause" a running container without losing any of its configuration. 

To see the containers that are currently running, we can use `docker ps`. We can also see all containers, including those that are stopped, using `docker ps -a`.

Another very useful command is `docker exec`, which allows us to run a command within a running container. This is very useful if we need to perform some configuration within the container itself, but we can also use it to open an interactive shell directly within a container. 

Finally, most applications running within Docker containers are configured to print logs directly to the terminal, and we can view that output using the `docker logs` commands. This is very helpful when a container isn't working like we expect, so we can explore the output produced by the application running in the container to help us debug the problem. 

---

Before we can start a container, we must find an image that we'd like to run. To do that, one of the first things we can do is just head to Docker Hub itself and start searching for an image. However, as we've already heard, there are other registries available, so if we can't find what we are looking for on Docker Hub, we may want to check sites such as GitHub or the application's website to learn about what images are available.

Once we've found an image we'd like to run, we need to consider a couple of other factors. First, images on Docker Hub and other registries are marked with various **tags**. The tags are used to identify the particular version or architecture of the image. So, let's take a look at the official image for Nginx to see what tags are available. (Navigate to [Nginx](https://hub.docker.com/_/nginx)). 

Here, we see many various versions of Nginx available, including images that are configured to include the `perl` module, and images based on the Alpine Linux project. If we scroll down the page a bit, we can see a discussion of the various image variants and how they differ. 

Most Docker images are based on one of the mainline Linux distributions, usually either Debian or Ubuntu. However, one of the image variants offered by Nginx, as well as many other applications, is based on the Alpine Linux project. Alpine is a very small Linux distribution that uses very compact libraries and doesn't include a lot of tools, making it ideal as a basis for very small Docker images. However, this can make it more difficult to work with Alpine-based images, since there aren't many tools included that can help with debugging. Likewise, building an image based on Alpine requires much more knowledge of the system and what libraries need to be included. 

Basically, if you aren't sure, it is generally best to go with an image based on a mainline Linux distribution you are familiar with. However, if you'd like to make your images as small as possible, you can choose to use an Alpine-based image instead.

Finally, if we scroll back to the top of the page, you'll see that the Nginx image is tagged as a "Docker Official Image" meaning that it is one of the curated repositories that has been reviewed by Docker and will generally be well maintained and updated. You can click on that tag to learn more, and even learn how to search Docker Hub for other official images. When in doubt, it is best to look for one of these official images anytime you want to use a particular application.

---

For this example, we're going to use another Docker Official Image called [Hello World](https://hub.docker.com/_/hello-world). This image is a great example of a minimal container, making it an easy place to get started with Docker. So, now that we've found the image we want to use, let's go back to the terminal and learn how to create and run some containers. 

[Demo Here]

---

There we go! That's a quick overview of using Docker to create and run containers. However, this small example leaves many questions unanswered! For example, how can we access our Nginx server outside of the Docker container itself? What if we want to host our own files in Nginx instead of the default webpage? Also, how can we store data from our containers so that it isn't lost each time the container restarts. And finally, is there a way to simplify these Docker commands so they are easy to replicate multiple times? 

Over the next few parts of this lab, we'll work on addressing each of these questions. 