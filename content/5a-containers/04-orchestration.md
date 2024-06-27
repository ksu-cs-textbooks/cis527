---
title: "Orchestration"
weight: 20
pre: "4. "
---

{{< youtube hPfXWL15M28 >}}

#### Resources

* **[Slides]({{% relref "./04-orchestration-slides.md"  %}})**
* **[Docker Tutorial for Beginners](https://www.youtube.com/watch?v=3c-iBn73dDE)** by TechWorld with Nana on YouTube
* [16 Best Container Orchestration Tools and Services](https://devopscube.com/docker-container-clustering-tools/) from DevopsCube
* [Docker Compose](https://docs.docker.com/compose) from Docker
* [Installing Docker Compose](https://docs.docker.com/compose/install/) from Docker
* [Compose File Specification](https://docs.docker.com/compose/compose-file/) from Docker

#### Video Transcript

Up to this point, we've only looked at how we can start and run containers one at a time on a single platform. While that is great for development and testing, we should know by now that manually doing anything in an enterprise situation is not a great idea. So, let's explore some of the methods and tools we can use to better orchestrate our containers and automate the creation and deployment of them.

Container orchestration is the overarching term I'll use for this concept, though it maybe isn't the most descriptive term. When are orchestrating containers, we are really talking about ways to manage and deploy containers at scale, sometimes on a single node, and sometimes across multiple nodes. For now, we'll only focus on a single node, and we'll address working with multiple nodes later in this module.

Orchestration also includes things such as managing the routing of network data and other resource between the various nodes, and possibly automating the ability to restart a node if it fails. 

In short, we want to take the same approach we took in Lab 2 related to building individual systems and apply that same idea to working with containers.

---

Here's a quick diagram showing what a full-fledge container orchestration setup might look like. At the top, we have a configuration file defining the architecture we want to deploy - in this case, a Docker Compose file, which is what we'll cover in this lesson. That file is then used to control multiple Docker engines running across multiple individual computing nodes, or servers on the cloud. This allows us to run containers across multiple nodes and handle situations such as load balancing and automated recovery in case of an error. 

Underneath the Docker engine, we may have multiple logical "clusters" of nodes or containers, which represent the different environments that our nodes are operating within. For example, we may have a test cluster and a production cluster, or our application may be separated across various physical or logical locations. 

Kubernetes follows a similar architecture, but we'll look at that more in depth later in this module.

---

So, for this example, let's look at another Docker tool, Docker Compose. Docker Compose is used to create various isolated Docker environments on a single node, usually representing various application stacks that we need to configure. Using Docker Compose, we can easily record and preserve the data required to build our container infrastructure, allowing us to adopt the "infrastructure as code" principle. Once we've created a Docker Compose file, we can easily make changes to the infrastructure described in the file and apply those changes to the existing setup. 

Finally, using Docker Compose makes it easy to move an infrastructure between various individual systems. A common use-case is to include a Docker Compose file along with a repository for a piece of software being developed. The Docker Compose file defines the infrastructure of other services that are required by the application, such as a database or message queue. 

---

The Docker Compose tool uses files named `docker-compose.yml` that are written using the YAML format. Inside of that file, we should see a `services` heading that defines the various services, or containers, that must be created. This particular file lists two services, `nginx` and `mysql`. Those second-level service names can be anything we want them to be, but I've found it is easiest to match them closely to the name of the Docker image used in the service. As a minimal example, each service here contains the name of a Docker image to be used, as well as a friendly name to assign to the container. So, this Docker Compose file will create two containers, one running Nginx and another running Mysql. It's pretty straightforward, but as we'll soon see, these files can quickly become much more complex.

---

Once we've created a Docker Compose file, we can use the `docker compose` commands to apply that configuration. Previously, `docker-compose` was a separate Docker client that was installed individually, but with the release of version 2.0 it was integrated within the main Docker client as a plugin. If you installed Docker Desktop, you should already have `docker compose` available as well, but if not you may have to install the Docker Compose plugin. The instructions for this are available in the links at the top of this page.

[demo here]

---

Once major feature of the Docker Compose file format that many users may not be aware of is the ability to `extend` a service definition from another file. This allows us to create individual files for each service, and them compose them together in a single `docker-compose.yml` file. We can also use this same technique to share some settings and configuration between many different services within the same file. 

In this example, we see our main `docker-compose.yml` file that contains a service definition for a webserver. That definition extends the basic `nginx` service that is contained in another file named `nginx.yml` in the same directory. Using this method, we can create multiple different web servers that all inherit the same basic `nginx` configuration, but each one can be customized a bit further as needed. This greatly reduces the amount of duplicated code between services, and can also help to greatly reduce the size of the main `docker-compose.yml` file for very complex setups.

---

There we go! That's a quick crash course in using Docker Compose to build a defined configuration for a number of Docker containers. For the rest of this lab, we'll mainly work in Docker Compose, but we'll show some basic Docker commands and how they compare to the same setup in Docker Compose. 