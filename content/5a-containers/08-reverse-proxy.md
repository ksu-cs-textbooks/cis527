---
title: "Reverse Proxy"
weight: 40
pre: "8. "
---

{{< youtube KEirdL6y6Nc >}}

#### Resources

* **[Slides]({{< relref "./08-reverse-proxy-slides.md" >}})**
* **[Docker Tutorial for Beginners](https://www.youtube.com/watch?v=3c-iBn73dDE)** by TechWorld with Nana on YouTube
* [Nginx Reverse Proxy](https://phoenixnap.com/kb/docker-nginx-reverse-proxy) from Phoenix NAP
* [Using Docker to Set up Nginx Reverse Proxy With Auto SSL Generation](https://linuxhandbook.com/nginx-reverse-proxy-docker/) from Linux Handbook
* [Docker Security](https://docs.docker.com/engine/security/) from Docker
* [Protect the Docker daemon socket](https://docs.docker.com/engine/security/protect-access/) from Docker
* [Docker Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html) from OWASP
* [Traefik Quickstart](https://doc.traefik.io/traefik/getting-started/quick-start/) from Traefik

#### Video Transcript

As we've seen, deploying services using Docker can make things very easy. Unfortunately, one major limitation of Docker is that the only way connect a running container to the outside world is by mapping a port on the host system to a port on the container itself. What if we want to run multiple containers that all host similar services, such as a website? Only one container can be mapped to port 80 - any other containers would either have to use a different port or be running on another host. Thankfully, one way we can get around this is by using a special piece of software known as a **reverse proxy**. In a nutshell, a reverse proxy will take incoming requests from the internet, analyze them to determine which container the request is directed to, and then forward that request to the correct container. It will also make sure the response from the container is directed to the correct external host. We call this a reverse proxy since it is acting as a connection _into_ our Docker network, instead of a traditional proxy that helps containers reach the _external_ internet.

As it turns out, the Nginx web server was originally built to be a high-performance reverse proxy, and that is still one of the more common uses of Nginx even today. In addition, there are many other Docker images that can help us set up and manage these reverse proxy connections. In this lesson, we'll review three different ways to create a reverse proxy in our Docker infrastructures.

---

The first option is to use Nginx directly. For this, we're going to set up a Docker Compose file that contains 3 different containers. First, we have a standard Nginx container that we are naming `proxy`, and we are connecting port 8080 on our host system to port 80 on this container for testing. In practice, we'd generally attach this container to port 80 on our host system as well. Notice that this is the only container connected to the `default` Docker network, so it is the only one that is meant to access the internet itself. Finally, we're using a bind mount on a volume that will contain a template configuration file for Nginx - we'll look at that a bit later.

The other two containers are simple `whoami` containers. These containers will respond to simple web requests and respond with information about the container, helping us make sure we are reaching the correct container through our reverse proxy. These two containers are both connected to the `internal` network, which is also accessible from the `proxy` container as well. 

---

To configure the Nginx server as a reverse proxy, we need to provide a template for configuration. So, inside of the folder mounted as a volume in the container, we need to create a file named `default.conf.template` that will be used by Nginx to generate it's configuration file. The contents of that file are shown here on the slide.

In effect, we are creating two different servers, one that listens for connections sent to hostname `one.local`, and the other will look for connections to `two.local`. Depending on which hostname is specified in the connection, it will forward those connections to either container `whoami1` or `whoami2`. We also include a bunch of various headers and configuration settings for a reverse proxy - these can be found in the Nginx documentation or by reading some of the tutorials linked at the top of this page.

---

So, now that we've set up our environment, let's get it running using `docker compose up -d`. After all of the containers are started, we can use `docker ps` to see that they are all running correctly. 

Now, let's test a connection to each container. We'll use the simple `curl` utility for this, and include the `-H` parameter to specify a hostname for the connection. So, by sending a connection to `localhost` on port `8080` with the hostname `one.local` specified, we should get a response from container `whoami1`. We can confirm that this is correct by checking the response against the output of `docker ps`. We can do the same to test host `two.local` as well. It looks like it is working!

So, with this setup in place, we can replace the two `whoami` containers with any container that has a web interface. It could be a static website, or an application such as PHPMyAdmin that we'd like to include as part of our infrastructure. By setting up a reverse proxy, we can access many resources on the same host and port, simply by setting different hostnames. So, all we'd need to do is register the various hostnames in our DNS configuration, just like we did when working with virtual hosts in Apache as part of Lab 5, and point them all at the same IP address where our Docker infrastructure is hosted. That's all it takes!

---

Another option for setting up a reverse proxy in Nginx is to use the `nginx-proxy` Docker image. This image includes some special software that can analyze our Docker configuration and automatically set up the various configurations needed for a reverse proxy in Nginx. This Docker Compose file shows the basic way this setup works.

First, we are creating a new Docker container named `proxy` based on the `nginx-proxy` image. We're still mapping port 80 inside of the container to port 8080 on our host system, and connecting it to the same networks as before. However, this time instead of mounting a volume using a bind mount that stores our Nginx configuration templates, we are creating a bind mount directly to the `docker.sock` socket. This is how the Docker client is able to communicate with the Docker engine, and we are effectively giving this Docker container access to the underlying Docker engine that it is running on. **This introduces a security concern, which we will address later in this lesson**.

The only other change is the environments for the two `whoami` containers. Notice that each container now contains a `VIRTUAL_HOST` and `VIRTUAL_PORT` entry, denoting the hostname that the container should use, and the port within the container where the connections should be sent to.

---

Now, when we bring up this infrastructure using `docker compose up -d`, we should be able to do the same test as before to show that the connections for `one.local` and `two.local` are being directed to the correct containers. As we can see here, it looks like it worked! But, how does `nginx-proxy` know how to configure itself?

Basically, the `nginx-proxy` software will inspect the configuration of the various containers available in the Docker engine, using the bind-mounted connection directly to the `docker.sock` socket. By doing so, it will see containers that have a `VIRTUAL_HOST` environment variable, and optionally a `VIRTUAL_PORT` variable, and it will configure a reverse proxy to that container using the hostname and port specified. So, if we add a third container to our Docker infrastructure, as long as it has a `VIRTUAL_HOST` environment variable set, `nginx-proxy` will automatically see it as soon as it starts, and it will set up a new reverse proxy to that container. This is very handy, as it allows us to start and stop containers as needed, and a reverse proxy will always be available without any additional configuration needed!

---

Unfortunately, as I mentioned earlier, there is a major security concern introduced when we allow a Docker container to have access to the `docker.sock` socket on the host system. As we already saw, this allows the software running in the Docker container to access the underlying Docker engine, which is great since it can basically perform all of the configuration we need automatically, and it can even detect when new containers are started.

However, there is nothing at all preventing the software in that container, or a malicious actor who has gained access inside of the container, from performing ANY other actions on the Docker engine. So, anyone with access inside of that container could start new containers, stop running containers, change the configuration of an existing container, and so much more.

In addition, in most installations the Docker engine runs as the `root` user of the host system! This means that anyone who has access to the Docker engine and armed with an unpatched flaw in Docker could easily gain root access to the entire host system! In short, if you have `root` access in a container that has access to the Docker socket, you can effectively end up with `root` access on the host system.

Obviously this is a very major security concern, and one that should definitely be taken into account when using Docker containers that need access to the underlying Docker engine. Thankfully, there are a few mitigation methods we can follow. For instance, we can protect access to the Docker socket with a TLS certificate, which prevents unauthorized access by any Docker clients who don't have the certificate. We can also protect access to the Docker socket by running it through a proxy that acts like a firewall, analyzing requests from Docker clients and determining if they are allowed. Finally, in many cases, we may not want to directly expose any container with access to the Docker engine directly to the internet itself, though in this case it would basically nullify the usefulness of Nginx Proxy.

So, it ends up being a bit of a tradeoff. If we want to use tools such as `nginx-proxy` in our environments, we'll have to analyze the risk that is presented by having the Docker engine available to that container, and either take additional precautions or add additional monitoring to the system. 

---

A third option for setting up a reverse proxy would be to use a Docker image designed specifically for that purpose. There are many of them available, but the most popular at this point is the Traefik Proxy server. Traefik Proxy is very similar to Nginx Proxy, since it also will examine the underlying Docker engine to configure reverse proxies. However, it includes many additional features, such as the ability to proxy any TCP request, introduce middleware, and automatically handle requesting TLS certificates from a provider like Let's Encrypt.

---

The Docker Compose file shown here is a minimal setup for the Traefik Proxy server. In the `proxy` container, we see that we are customizing the startup command by providing two options, `--api.insecure=true` and `--providers.docker`. This will allow us to access the Traefik Proxy dashboard, and tells Traefik to look at Docker for information about proxies to be created. We're also mapping two ports to the Traefik proxy - first we are connecting port 8080 on the host to port 80 on the proxy, which will handle HTTP traffic. In addition, we are connecting port 8081 on the host to port 8080 inside of the container, which is the port where we can access the Traefik Proxy dashboard. We'll take a look at that a bit later.

Then, we set up two `whoami` images just like before. However, this time, instead of setting environment variables, we add a couple of labels to the containers. These labels are used to tell Traefik Proxy what hostname and port should be used for the reverse proxy, just like we saw earlier in our configuration for Nginx Proxy.

---

So, just like before, we can use `docker compose up -d` to start these containers. Once they are up and running, we can once again use `docker ps` to see the running containers, and we can use `curl` to verify that the proxy is working and connecting us to the correct containers. 

---

To explore the configuration of our Traefik Proxy, we can also load the dashboard. To do this, we'll simply open a web browser and visit http://localhost:8001. This slide shows a screenshot of what it may look like for our current configuration.

Just like with Nginx Proxy, Traefik will automatically add proxy routes for any new containers that have the correct labels, and we can see them update here on this dashboard in real time. Of course, right now this dashboard is completely unsecured and totally open to anyone who has access to our system, so in practice we'll probably want to secure this using some form of authentication. The Traefik Proxy documentation includes information for how to accomplish that. 

---

So, in summary, setting up a reverse proxy is a great way to allow users from the outside internet to have access to multiple servers running on the same Docker host. In effect, we are able to easily duplicate the features of Virtual Hosts in traditional webservers, but instead of loading files from a different directory, we are directing users to a different Docker container inside of our infrastructure. 

We looked at three reverse proxies - Nginx itself, Nginx Proxy, and Traefik Proxy. Of course, there are many others out there that we can choose from - these are just three that are pretty well known and used often today.

Finally, it is worth noting that a reverse proxy such as this is generally only needed for Docker containers hosted on a single host. If we choose to use orchestration platforms such as Kubernetes, much of this is handled by the platform itself. So, in the next lesson, we'll explore Kubernetes a bit and see how it differs from what we've seen so far in Docker.