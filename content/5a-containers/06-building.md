---
title: "Building Images"
weight: 30
pre: "6. "
---

{{< youtube _bkZrMqqoZY >}}

#### Resources

* **[Slides]({{< relref "./06-building-slides.md" >}})**
* **[Docker Tutorial for Beginners](https://www.youtube.com/watch?v=3c-iBn73dDE)** by TechWorld with Nana on YouTube
* [Docker Get Started Tutorial](https://docs.docker.com/get-started/) from Docker
* [Docker Sample Node Application](https://github.com/docker/getting-started/tree/master/app) from Docker on GitHub
* [Docker Language Specific Guides](https://docs.docker.com/language/) from Docker
* [GitHub CI Example](https://github.com/russfeld/ksucs-hugo) (the sample site for this textbook's theme)
* [GitLab CI Example](https://gitlab.cs.ksu.edu/cis-527) (this textbook)

#### Video Transcript

So far, we've explored how to download and use pre-built Docker images in our infrastructure. In many cases, that covers the vast majority of use cases, but what if we want to build our own Docker images? In this lesson, we'll explore the process for creating our own Docker images from scratch. The process is pretty simple - we start with a special file called a `Dockerfile` that describes the image we want to create. In that file, we'll identify a base image to build on, and then include information to configure that image, add our software and configure it, and then set some last details before building the new image. So, let's see how that process works in practice!

---

Normally, we'd probably have our own application that we want to include in the Docker container. However, since this is a course on system administration, we're going to just use a sample program provided by Docker itself as the basis for our image. So, you can follow along with this entire tutorial by going to the Docker Get Started documentation that is at the URL shown on this slide. We'll basically be following most of the steps in that tutorial directly.

---

Our first step is to get a copy of the application code itself. So, on one of our systems that has Docker installed and configured, we can start by cloning the correct repository, and then navigating to the `app` directory inside of that repository. At this point, we may want to open that entire directory in a text editor to make it easy for us to make changes to the various files in the application. I'm going to open it in Visual Studio Code, since that is what I have set up on this system.

---

Now that we have our application, we can create a `Dockerfile` that describes the Docker image that we'd like to create that contains this application. This slide shows the `Dockerfile` from the tutorial. Let's go through it line by line to see what it does.

First, we see a `FROM` line, which tells us what base image we want to build the image from. In this case, we have selected the `node:12-alpine` image. Based on the context, we can assume that this is a Docker image containing Node.js version 12, and that it was originally built using the Alpine Linux project, so the image is a very minimal image that may not have many additional libraries installed. This also tells us that we'll need to use commands relevant the Alpine Linux project to install packages, so, for example, we'll need to use `apk add` instead of `apt install`.

The next line is a `RUN` command, which specifies commands that should be run inside of the image. In this case, we are installing a couple of libraries using the `apk add` command. Since this command will change the filesystem of the image, it will end up generating a new **layer** on top of the `node:12-alpine` image. 

Next, we have a `WORKDIR` entry, which simply sets the working directory that the next commands will be run within. So, in this case, we'll be storing our application's code in the `/app` directory within the Docker image's file system.

After that we, see a `COPY` command. This one is a bit confusing, since the copy command in a Dockerfile operates in two different contexts. The first argument, `.` is interpreted within the host system, and references the current directory where the `Dockerfile` is stored. So, it will in effect copy all of the contents from that directory into the Docker image. The second argument, also a `.`, is relative to the Docker image itself. So, these files will be placed in the current directory in the Docker image, which is `/app` based on the `WORKDIR` entry above. As you might guess, this also creates a new **layer** in our created Docker image.

Once we've loaded our application files into the image, we see another `RUN` command. This time, we are using the `yarn` package manager to install any libraries required for our Node.js application to function. If you are familiar with more recent Node.js applications, this is roughly equivalent to the `npm install` command for the NPM package manager. This creates a third new **layer** in our resulting image.

Finally, we see two entries that set some details about the final image itself. The first entry, `CMD` will set the command that is executed when a container is instantiated using this Docker image. Since we are building a Node.js application, we want to use the `node` command to run our server, which is stored in the `src/index.js` file. Notice that this command is also relative to the `WORKDIR` that was given above!

Finally, we have an `EXPOSE` entry. This simply tells Docker that the port that should be made available from a container instantiated using this image is port 3000. However, by default this won't actually create a port mapping to that port - we still have to do that manually! However, there are some tools that can use this information to automatically route data to the Docker container itself, and this `EXPOSE` entry helps it find the correct port to connect to.

There we go! That's a basic `Dockerfile` - it may seem a bit complex, but when we break it down line by line, it is actually very simple and easy to understand.

---

So, once we've created a `Dockerfile` for our project, we can use the `docker build` command to actually build our Docker image. In that command, we can use the `-t` argument to "tag" the image with a simple to understand name so we can easily reference it later. We also need to specify the location of the `Dockerfile`, which is why we include the `.` at the end of the command.

Once our Docker image is built, we can use a simple `docker run` command to instantiate a container based on that image. We'll also map port 3000 so we can access it from our local machine. If everything works, we can go to a web browser and visit http://localhost:3000 to see our application running!

---

Now that we've built and run our Docker image, let's make a quick update to the code and see how easy it is to rebuild it and run it again. First, we'll make a quick edit in the `app.js` file to change a line of text. Then, we'll use `docker build` to rebuild the Docker image. Take note of how long it takes to rebuild that image - we'll try to make that faster a bit later!

Once it is built, we are ready to use it to instantiate a container. However, before we can run it, we must stop the running container that was built from the previous image using `docker stop`, and then we can use `docker run` to instantiate a new container. 

---

At this point, we have a working Docker image that includes our application, but it is just stored on our own computer. If we want to share it with others, we have to upload it to a registry such as Docker Hub. If the project is hosted on GitHub or GitLab, we can use the various continuous integration and delivery features of those tools to automatically build our image and then host it on their registries as well. You can refer to the documentation for various registries if you are interested in hosting your image there. You can also look at some example CI/CD pipelines for both GitHub and GitLab by following the links at the top of this page. 

---

Another task we may want to do after building our image is scanning it for vulnerabilities. Docker includes a quick scanning tool `docker scan` that will look at the image and try to find various software packages that are vulnerable. It is even able to look at things such as the `package.json` file for Node.js applications, or the `requirements.txt` file for various Python programs, among others. 

As we can see on this slide, the current version of the Getting Started application actually includes a number of vulnerabilities introduced by an older version of a couple of Node.js libraries, so we may want to work on fixing those before we publish our image. 

Likewise, when we download an image from a registry, we may want to scan it first to see what vulnerabilities may be present in the image before we run it. Of course, this isn't able to catch **all** possible vulnerabilities, but it is a good first step we can use when reviewing Docker images. 

---

Finally, let's take a minute to look at the structure of our `Dockerfile` and see if we can do something to improve it a bit. Previously, our `Dockerfile` basically created three new layers on top of the base image - one to install packages in the operating system itself, one to add our application files, and a third to install packages for the Node.js environment that our application uses. Thankfully, Docker itself is very good about how it manages layers on an image, and if it is able to determine that a layer can be reused, it will pull that layer from the cache and use it instead of rebuilding it. So, as long as we start with the same base image and install the same software each time, Docker will be able to use that layer from the cache. So, our first layer can easily be loaded from the cache!

 However, each time we change any of the code in our application, we will end up having to rebuild the last two layers, and that can greatly slow down the process of building a new image. Thankfully, by changing our `Dockerfile` just a bit, as shown on this slide, we can take advantage of the caching capability of Docker to make subsequent builds much easier. In this case, we start by just copying the `package.json` and `yarn.lock` files to the image, and then run `yarn install` to install the libraries needed for our application. This will populate the `node_modules` folder, and it creates a new layer for our image. That layer can be cached, and as long as we don't make any changes to either the `package.json` or `yarn.lock` files in our application, Docker will be able to reuse that cached layer!

 From there, we can copy the rest of our application files into the image and then we are good to go. However, since we've already installed our libraries, we don't want to overwrite the `node_modules` folder. So, we can create a special file named `.dockerignore` to tell Docker to ignore various files when creating our image. It works the same way as a `.gitignore` file. So, we can just tell Docker to ignore the `node_modules` folder when it copies files into our image!

 Try it yourself! Build an image with this new `Dockerfile`, then make a change somewhere in the application itself and rebuild the image. You should now see that Docker is able to reuse the first two layers from the cache, and the build process will be much faster. So, by thinking a bit about the structure of our application and how we write our `Dockerfile`, we can make the build process much more efficient.

 Docker has some language-specific guides in their documentation that give `Dockerfile` examples for many common languages, so you can easily start with one of their guides whenever you want to build your own images. The Docker extension for Visual Studio Code also has some great features for building a `Dockerfile` based on an existing project. 
 
 That should give you everything you need to start building your own Docker images!