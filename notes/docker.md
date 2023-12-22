# Docker

Docker is an excellent tool for managing and deploying microservices. Each microservice can run in a separate Docker container.

Docker is a containerization software designed to create, deploy, and run your application inside of a container. Containers are designed to encapsulate a specific application and its dependencies, not an entire operating system. Instead of containing a full operating system, a container shares the host operating system's kernel.

- Hypervisor creates and runs virtual machines.
- Docker Engine creates and runs containers.
- Virtual machines and containers are instances of their corresponding images (read-only templates).

Docker was initially developed for and is closely associated with Unix-based systems, specifically Linux. Docker has expanded its support to other operating systems, including Windows and macOS, through additional technologies and integrations.

- **Windows** - Docker Desktop for Windows uses Hyper-V virtualization to create a Linux-based virtual machine, allowing you to run Linux containers on a Windows host. It uses a lightweight Linux subsystem called WSL 2 (Windows Subsystem for Linux) to run Linux containers. It also supports Windows containers, which use Windows-native containerization technology.

- **macOS** - Docker Desktop for macOS uses HyperKit, a lightweight hypervisor for macOS, to run a small Linux VM. Like the Windows version, it enables you to run Linux containers on a macOS host.

Docker is used to containerize background applications and CLI programs. You can use Docker with network applications like web servers, databases, and mail servers and with terminal applications like text editors, compilers, network analysis tools, and scripts.

In some cases, it’s even used to run GUI applications like web browsers and productivity software. You can either use an existing X Server, where the host machine is already running a graphical environment, or you can run a VNC server within the container.

## Docker Architecture

![[docker-architecture.png]]

**Docker Daemon (dockerd)** - Background process that manages Docker containers on a host system. It listens for Docker API requests and manages Docker objects, such as images, containers, networks, and volumes. The daemon runs on the host machine, and clients communicate with it to perform various Docker-related tasks.

**Docker Client (docker)** - Command-line tool or a RESTful API client that allows users to interact with the Docker daemon. Users issue commands to the Docker client, which then communicates with the Docker daemon to carry out the requested actions.

**Docker Registry** - Centralized repository that stores Docker images. Docker Hub is the default public registry, but private registries can also be used to store and distribute custom images.

## Containers & Virtual Machines

### Containers

- Containers provide a way to virtualize an OS so that multiple workloads can run on a single OS instance.
- Each container shares the host OS kernel and, usually, the binaries and libraries, too.
- Containers are usually only megabytes in size and take just seconds to start.

### Virtual Machines

- VMs provide a way to virtualize the hardware to run multiple OS instances.
- Each VM has its own OS, with binaries, libraries, and applications.
- VMs may be many gigabytes in size, and take some time to start

Unlike a virtual machine, rather than creating a whole virtual operating system, Docker allows applications to use the same Linux kernel as the underlaying system and only requires applications be shipped with components missing on the host computer

## Docker Image & Docker Container

Docker **image** is an executable package that includes everything needed to run an application, including the code, a runtime, libraries, environmental variables and configuration files. A **container** is a runtime instance of an image.

## Docker Workflow

1. Create a new directory and CD into it
2. Create a Dockerfile (contains commands for the Docker on how to build an image)
3. Run the following command to build the Docker image. The -t flag lets you tag your image so it's easier to find:
   1. `$ docker build -t  .`
4. Create a named container from that image:
   1. `$ docker create --name`
5. Start (execute) the container in the interactive mode (-i, the output is streamed to your terminal):
   1. `$ docker start -i`
6. If the container runs continuously, you can stop it with: $ docker stop You can also create and start the container with one instruction:
   1. `$ docker run` OR `$ docker run -i`

### Create the Dockerfile

An image is created based on instructions found in Dockerfile. Each Dockerfile instruction will generate a new read-only layer on top of the last one. Dockerfile always starts with a FROM instruction that pulls a base image from the local disk or remote repository to start with. Then, you customize (configure) the base image by adding other binaries, dependencies, defining env variables and copying your app from your computer's filesystem to a directory in the image. Finally, you define which instruction is going to be executed within the container when it starts.

![[create-the-dockerfile.png]]

### Create the Image

When an image is being created (built) using the $ docker build command, each Dockerfile instruction generates a new read-only layer on top of the last one.

Once you have created the image, you can ispect it by using Docker Dashboard. Go to the image list and select 'Inspect' from the image menu.

### Create the Container

When a container is created using the $ docker create command on the image, a new writeable layer that stacks on top of the image layers is created. This writeable layer allows to make changes to the container.

![[create-the-container.png]]

## Dockerfile Instructions

- **FROM** - Initializes a new build stage and sets the Base Image for subsequent instructions. A Dockerfile must start with a FROM instruction. The image can be any valid image. Usually this is an image pulled from the Public Repositories.

- **ADD** - Copies a file into the image but it also supports tar and remote URL's.

- **COPY** - Copies local computer files into the image and it's preferred over ADD for its simplicity unless you need the features of ADD which include tar and remote URL support.

- **RUN** - Executes any commands during the build time in a new layer, on top of the current image and commits the results. The resulting committed image is used for the next step in the Dockerfile. This is mainly used for installing a new package into your image.

  - Every RUN adds a new layer on top of an existing image or OS distribution. OS distribution is the initial image and every package is added as a new layer on top of that.

- **WORKDIR** - Sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD instructions that follow it in the Dockerfile.

- **ENV** - Sets the environment variable. This value will be in the environment for all subsequent instructions in the build stage.

- **ENTRYPOINT** - Specifies the instruction that is to be executed when a Docker container starts. In comparison to CMD, it cannot be overridden by docker run. Whatever is specified in docker run will be appended to ENTRYPOINT (this is not the case with CMD).

- **CMD** - Specifies the instruction that is to be executed when a Docker container starts. In comparison to ENTRYPOINT, can be overridden by docker run.

- **EXPOSE** - Informs Docker that the container listens on the specified network ports at runtime.

- **VOLUME** - Creates a mount point as defined when the container is run. Volumes are the preferred mechanism for persisting data generated by and used by Docker containers. Volumes are completely managed by Docker, meaning, the volume’s content exist inside a dedicated Docker area which is part of the underlying OS filesystem.

## Docker Compose

**Docker Compose** is a tool used for defining and running multicontainer Docker applications.

With Compose, you use a **YAML** file to define & configure your application’s services. Then, with a single command, you create and start all the services from your configuration as separate containers.

Using Compose is basically a three-step process:

1. For every service, define the Dockerfile so it can be reproduced anywhere.
2. Define the services that make up your app in compose.yml so they can be run together in an isolated environment.
3. Lastly, run docker compose up and Compose will start and run your entire app.

### compose.yml

The file is usually organized into three sections. You need to specify at least one **service**. The sections **volumes** and **networks** are optional.

- **services** - In Docker, a service is the name for a container in production. This section defines the containers that will be started as a part of the Docker Compose instance.

- **networks** - This section is used to configure networking for your application. You can change the settings of the default network, connect to an external network, or define app specific networks.
- **volumes** - Mounts a linked path on the host machine that can be used by the container.

**NOTE 1:** Use only 'space' key to align yml entries. yml will not work if entries, including the nested ones, are not aligned. Make sure you always use the same number of spaces to align directives

**NOTE2:** If run locally, on the same network, Docker makes sure that the containers are able to talk with each other, without specifiying the 'networks' section.

### Services

**Services** refer to containers' configuration. For example, let's take a dockerized web application consisting of a frontend, a backend, and a database.

We need to define 3 different services (containers) that will be created from specific images. Sometimes, the image we need for our service has already been published (by us or by others) in Docker Hub, or another Docker Registry.

In that case, we use the image directive to specify the image name and tag. If we need to build an image from our source code by reading its Dockerfile, we use the build directive passing the path to the Dockerfile as the value.

If image directive is used with build, then, the image directive gives a name the image created.

Here are some of the common services directives used to set up and configure containers:

- **build** - This directive can be used instead of image. Specifies the location of the Dockerfile that will be used to build this container.

- **image** - Sets the image that will be used to build the container. Using this directive assumes that the specified image already exists either on the host or on Docker Hub.

- **container_name** - Specifies a custom container name, rather than a generated default name
- **restart** - Configures the restart policy for a container.

- **depends_on** - Sets a service as a dependency for the current block-defined container. Compose always starts and stops containers in dependency order.

- **port** - Maps a port from the container to the host in the following manner: host:container.

---

To create and run your multi-container app, execute the following from the directory that contains the yml file (runs it in the detached mode, -d, in the background).

`$ docker compose up –d`

- This creates and runs two images: **db**, **adminer**

The images are being pulled from the Docker Hub, created and executed in their own containers. Use Docker Desktop to inspect those OR execute the following to see them listed.

`$ docker images` OR $ `docker ps`

Open the browser and navigate to localhost:8013 to see adminer in action.

Stop the running containers from Docker Decktop OR CLI:

`$ docker compose stop`

Remove the stopped containers from Docker Decktop OR CLI:

`$ docker compose rm -f`
