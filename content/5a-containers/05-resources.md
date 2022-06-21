---
title: "Resources"
weight: 25
pre: "5. "
---

{{< youtube f0yYNe1Ip-4 >}}

#### Resources

* **[Slides]({{< relref "./05-resources-slides.md" >}})**
* **[Docker Tutorial for Beginners](https://www.youtube.com/watch?v=3c-iBn73dDE)** by TechWorld with Nana on YouTube
* [Networking Containers](https://docs.docker.com/engine/tutorials/networkingcontainers/) from Docker
* [Docker ARG, ENV, and .env - A Complete Guide](https://vsupalov.com/docker-arg-env-variable-guide/) by Vladislav Supalov
* [Docker Storage Overview](https://docs.docker.com/storage/) from Docker (_contains information about choosing different storage types_)
* [Docker Bind Mounts](https://docs.docker.com/storage/bind-mounts/) from Docker
* [Docker Volumes](https://docs.docker.com/storage/volumes/) from Docker

#### Video Transcript

So far we've learned how to pull Docker images from a repository and instantiate them as containers, and also how to use Docker Compose to achieve the same result, but we really haven't been able to do much with those containers. That's because we haven't given our containers any resources to work with. So, let's do that now.

There are many different resources that can be assigned to containers. We can connect a network port from our host system to a network port on a container, allowing external access into the container from the network. We can also attach containers to various internal networks, allowing specific containers to talk with each other directly. In addition, we can set specific environment variables within a container, which are primarily used by the applications running within the container as configuration parameters, specifying things such as usernames, passwords, and other data needed by the container. Finally, we can attach a storage volume to a container, allowing us to store and persist data even after a container is stopped. 

---

Let's start with the most common container resource - the networked port. This diagram shows a high-level overview of how this works. Inside of Docker, we might have two containers, one running a database server and the other hosting a web server. Since we want external users to be able to talk to the web server, we can map a network port from our host system, represented by the outer box, to a port on the web container. In this case, we are connecting the external port 8000 with the internal port 5000 on the `web` container. So, any incoming network traffic to our host on port 8000 will be forwarded to port 5000 on the web container.

---

To do this in Docker, we can use the `-p` flag on the `docker run` command to map a port from the host system to a container. The syntax of this command puts the external port first, then the port on the container. So, in this command, we are connecting port 8080 on our system to port 80 inside the Nginx container. 

Below, we see the same system defined in Docker Compose as well. It adds a `ports:` entry below the service definition, and uses the same syntax as the `docker run` command. Of course, in both cases we can map multiple ports inside of the container by supplying additional `-p` entries in `docker run` or by adding additional elements below the `ports:` entry in Docker Compose.

So, let's give this a try and then show that we can access the webserver from outside the container.

[demo here]

---

Once we've mapped a port on a container, we can use the `docker ps` command to see the various port mappings present on a container. This is a great way to quickly confirm that we mapped the port correctly. I still sometimes get my ports reversed, so this is a quick and easy way to confirm it is set up properly when I'm debugging problems in a container.

---

Next, lets go from individual ports to entire networks. We can expand the previous example by moving the `db` container to a separate network within Docker, isolating it from other containers and possibly even the outside world by making the new network internal to Docker. 

--

To do this using the Docker client, we can start by creating our container using the `docker run` command. This will connect the container to the default network in Docker - any container that is started without defining a network will be automatically connected to the default network.

However, we can create a new network using the `docker network` command as shown here. This will create a new bridge network named `redis_network`, and it also specifies that it is an `internal` network, meaning that it won't be connected to the outside world at all. 

Once we've created the network, we can attach any existing containers to that network using the `docker network connect` command.

We can also use the `--network` flag in the `docker run` command automatically connect a container to a defined network when we create it. However, it is worth noting that this has two caveats:

1) The container will not be connected to the default Docker network
2) We can only specify one network in the `docker run` command. If we want the container to be attached to multiple networks, we have to attach the rest manually using the `docker network connect` command.

---

This Docker Compose file shows the same basic setup as the previous set of Docker commands We start by creating an `nignx` service that is connected to both the `default` and `redis` networks, and it has a port mapping to the outside world. Then, the `redis` service is only connected to the `redis` network. Finally, at the bottom of the file, we see a new top-level entry `networks` that lists the networks used by this configuration. Notice that we don't have to include the `default` network here, since it is created for us automatically, though we can list it here if we want to configure it beyond the default settings.

So, let's go ahead and apply this Docker Compose file to see it in action.

[demo here]

---

Once we've got our containers running, we can use the `docker network inspect` command to inspect the various networks on our system. If we scroll through the output, we can find the containers connected to each network, as well as other information about how the network is configured. We can also test and make sure the containers can talk with each other, though we'll leave that to a later example.

---

Another resource we can give to our Docker containers are environment variables. Many applications that are developed to run in Docker containers use environment variables for configuration. A great example of this is the MySQL Docker image - when we create a container from that image, we can provide a root password for the database as an environment variable. We can also use it to configure a second account and database, making it quick and easy to automate some of the basic steps required when setting up a database for an application. This diagram shows some of the places where environment variables are used in the process of building and instantiating a Docker container.

---

So, let's see what that looks like in practice. Here is a set of `docker` commands that can be used to create two containers - one containing a MySQL database server, and another containing PHPMyAdmin, a program for managing MySQL databases. In both of the `docker run` commands, we are including an environment variable using the `-e` flag. For MySQL, we are setting a root password. Then, for the PHPMyAdmin container, we are configuring the hostname where it can find the MySQL server. Notice that the hostname we are giving it is the name of the MySQL container we created earlier, `mysql1`. This is one of the coolest aspects of networking in Docker! Docker actually handles an internal form of DNS for us, so each Docker container on a network is accessible by simply using the container name as the full hostname on the Docker network. This makes it super simple to connect Docker containers together in a network!

---

This slide shows the same basic setup in a Docker Compose file. Just like we specify ports and networks in the YML format, we can add another entry for `environment` that lists all of the environment variables. So, as before, we can create a `docker-compose.yml` file containing this content, and then use the `docker compose up -d` command to bring up this configuration in Docker. Let's do that now to see how it works.

[demo here]

---

We can also explore our running Docker containers to find the various environment variables that are available to that container. We can use the `docker inspect` command to inspect the configuration of each individual container. Of course, this presents a unique security vulnerability - notice here that we can easily see the root password for our MySQL server in our Docker environment. This is not good! If anyone has access to the Docker engine, they can potentially find out tons of sensitive information about our containers! So, we should think very carefully about what information we put in the environment variables, and who has access to the Docker engine itself. Thankfully, for orchestrating containers across the network, tools such as Kubernetes include a way to secure this information, so it is less of a concern there.

---

Now that we have a running MySQL server, along with PHPMyAdmin, let's take a minute to set up a database and store some information in it.

[demo here]

Now that we've stored some information in this database, let's stop and restart the container and see what happens.

[demo here]

Uh oh! Our information disappeared! This is because the transient read/write layer of a container is discarded when it is stopped, so any changes to the filesystem are not kept. While this is a great feature in many ways, it can also cause issues if we actually want to save that data!

---

Docker includes two different ways we can store data outside of a container. The first is called a **bind mount**, which simply connects a directory on our host's filesystem to a folder path in the container. Then, any data in the container that is written to that folder is actually stored in our host's filesystem outside of the container, and it will be available even after the container is stopped. 

The other method we can use is a Docker volume. A Docker volume is a special storage location that is created and managed by Docker itself. We can think of it like a virtual hard disk that we would use with VMWare - it is stored on the host filesystem, but it isn't directly accessible outside of Docker itself. 

There are many pros and cons for using both bind mounts and volumes in Docker - it really depends on how you intend to use the data. See the Docker documentation for a good discussion about each type of storage and the use-cases where it makes the most sense.

---

To use a bind mount in Docker, we must first make sure the folder exists in our host filesystem. For this, I'm just going to use the `mkdir` command to make the directory. We can then add a `-v` parameter to our `docker run` command. The first part of the volume entry is the path to the directory on the host system, and then following a colon we see the path within the container's filesystem where it will be mounted. This is a very similar syntax to the port mappings we learned about earlier. At the bottom of this slide, we see the same configuration in Docker compose - we simply add a `volumes` entry and list the bind mount there.

---

To use a volume in Docker, the process is very similar. First, we can use the `docker volume create` command to make a volume in Docker. Then, in our `docker run` command, we use the name of the volume as the first part of the `-v` parameter, followed by the path inside of the container where it should be mounted. 

In Docker Compose, the process is very similar. However, in this case, we don't have to manually use the `docker volume create` command, as Docker Compose will handle creating the volume for us. 

One thing to be aware of is where the volume is mounted within the container. Many Docker images, such as MySQL, include notes in the documentation about where data is stored in the container and which directories should be mounted as volumes to persist the data. So, in this case, the `/var/lib/mysql` directory in the container is the location given in the MySQL Docker Image documentation for persistent storage, so that's why we are mounting our volume in that location.

So, let's update our MySQL container to include a volume for storing data. Once we do that, we'll show that it will properly store and persist data.

[demo here]

---

Finally, just like any other resource, we can use the `docker inspect` commands to see the volumes and bind mounts available on a container. 

---

There we go! That's a pretty in-depth overview of the various resources that we can add to a Docker container. We've learned how to map ports from the host system to ports within a container, connect containers together via various Docker networks, provide data to Docker containers in environment variables, and finally we can now persist data using bind mounts and Docker volumes. At this point, we should have enough information to really start using Docker effectively in our infrastructures. For the rest of this module, we'll dive into various ways we can use Docker and more advanced configurations. 