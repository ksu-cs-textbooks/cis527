---
title: "Resources"
weight: 25
pre: "5. "
---

{{< youtube >}}

#### Resources

* **[Slides]({{< relref "./05-resources-slides.md" >}})**
* **[Docker Tutorial for Beginners](https://www.youtube.com/watch?v=3c-iBn73dDE)** by TechWorld with Nana on YouTube
* [Networking Containers](https://docs.docker.com/engine/tutorials/networkingcontainers/) from Docker
* [Docker ARG, ENV, and .env - A Complete Guide](https://vsupalov.com/docker-arg-env-variable-guide/) by Vladislav Supalov
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

