---
title: "Developing with Containers"
weight: 35
pre: "7. "
---

{{< youtube >}}

#### Resources

* **[Slides]({{< relref "./07-developing-slides.md" >}})**
* **[Docker Tutorial for Beginners](https://www.youtube.com/watch?v=3c-iBn73dDE)** by TechWorld with Nana on YouTube
* [Docker in Visual Studio Code](https://code.visualstudio.com/docs/containers/overview) from Visual Studio Code
* [Developing Inside a Container](https://code.visualstudio.com/docs/remote/containers) from Visual Studio Code
* [Remote Development in Containers Tutorial](https://code.visualstudio.com/docs/remote/containers-tutorial) from Visual Studio Code
* [GitHub CI Example](https://github.com/russfeld/ksucs-hugo) (the sample site for this textbook's theme)
* [GitLab CI Example](https://gitlab.cs.ksu.edu/cis-527) (this textbook)

#### Video Transcript

Docker is obviously a very useful tool for system administration, as we've seen throughout this module. In this lesson, however, let's take a minute to talk about how we can use Docker in the context of software development. Depending on the application we are developing and how it will eventually be packaged and deployed, Docker can be used at nearly every stage of the development process.

---

First, for applications that may be packaged inside of a Docker image and deployed within a container, we may wish to create a `Dockerfile` and include that as part of our source code. This makes it easy for us to use Docker to run unit tests in a CI/CD pipeline, and we can even directly deploy the finalized image to a registry once it passes all of our tests. 

This slide shows a sample `Dockerfile` for a Python application written using the Flask web framework. It is very similar to the Node.js example we saw earlier in this module. By including this file in our code, anyone can build an image that includes our application quickly and easily.

---

Another great use of Docker in software development is providing a `docker-compose.yml` file in our source code that can be used to quickly build and deploy an environment that contains all of the services that our application depends on. For example, the Docker Compose file shown in this slide can be included along with any web application that uses MySQL as a database. This will quickly create both a MySQL server as well as a PHPMyAdmin instance that can make managing the MySQL server quick and easy. So, instead of having to install and manage our own database server in a development environment, we can simply launch a couple of containers in Docker.

In addition, this file can be used within CI/CD pipelines to define a set of services required for unit testing - yet another way we can use the power of Docker in our development processes.

---

A more advanced way to use Docker when developing software is to actually perform all of the development work directly within a Docker container. For example, if we are using a host system that has one version of a software installed, but we need to develop for another version, we can set up a Docker container that includes the software versions we need, and then do all of our development and testing directly within the container. In this way, we are effectively treating it just like a virtual machine, and we can easily configure multiple containers for various environments quickly and easily.

The Visual Studio Code remote extension makes it easy to attach to a Docker container and run all of the typical development tools directly within a container. For more information about how that works, see the links in the resources section at the top of this page. 

---

Finally, as I've alluded to many times already, we can make use of Docker in our continuous integration and continuous delivery, or CI/CD, pipelines. Both GitHub and GitLab provide ways to automate the building and testing of our software, and one of the many tasks that can be performed is automatically creating and uploading a Docker image to a registry. This slide shows an example of what this looks like using GitHub actions. All that is required is a valid `Dockerfile` stored in the repository, and this action will do the rest.

---

Similarly, GitLab allows us to create runners that can automate various processes in our repositories. So, this slide shows the same basic idea in a GitLab pipeline. In fact, this pipeline will be run within a Docker container itself, so we are effectively running Docker in Docker to create and push our new Docker image to a registry.

At the top of this page are links to a couple of sample repositories that contain CI/CD pipelines configured in both GitHub and GitLab. In each repository, the pipeline will create a Docker image and publish it to the registry attached to the repository, so we can easily pull that image into a local Docker installation and run it to create a container.

---

This is just a small sample of how we can use Docker as a software developer. By doing so, we can easily work with a variety of different services, automate testing and packaging of our software, and make it easy for anyone else to use and deploy our applications within a container. So, I highly encourage you to consider integrating Docker into your next development project. 