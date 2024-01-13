---
title: "Containers and virtualization with Docker"
datePublished: Fri Jul 14 2023 14:52:04 GMT+0000 (Coordinated Universal Time)
cuid: clk2p6mdp00020al1cnva0mff
slug: containers-and-virtualization-with-docker
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1689346313150/d139aef4-2ea9-4998-90a2-c8d6d4134633.png

---

## Docker containers

Docker is an open-source software for the deployment of containerised applications. Docker containers are running Docker images/Linux images that can pack the code of a project and all its dependencies. It allows for cross-platform development and forms the elemental unit called a pod for container orchestration software like the Kubernetes engine.

## Virtual machines Vs. Docker

An Operating system consists of two stacked layers.

Going from top to bottom, we first encounter the OS Applications layer, which consists of all the software run on the machine.

Secondly, we get the OS kernel, the layer that deals with communication with hardware resources, and acts as a bridge between the hardware and the OS Applications layer.

A virtual machine emulates both the OS kernel and the applications layer stacked in the mentioned order. On the other hand, containerisation tools like Docker and Podman use the host's kernel.

### The advantage of Docker

With the added advantage of using the host's kernel, Docker containers save on resources and boost up speed. Docker is used specifically because it's one of the most popular tools in its category, also its registry, Docker-Hub is one of the largest repositories for pulling dependencies for your project.

## A small problem

Despite its advantages in shipping and replicating project environments. Docker needs a Linux kernel to run, this means that on non-linux distributions like Windows, we need to have a virtualized kernel. (WSL-2 or Hyper-V in this case). This means that even though the speed of firing up the containers may not be affected, the resource footprint is not far from that required by a typical VM.

## Spinning up a new container

Docker can be installed through the official set of instructions on their [site](https://docs.docker.com/engine/install/).

It uses the Docker engine which the docker daemon responsible for all processes concerning it.

There are two options, one is to either pull an existing container through Docker's registry called [Docker Hub](https://hub.docker.com/). Secondly is to build custom images to suit our project's needs.

### Using existing images

To clone a docker container off Docker Hub,

```dockerfile
docker pull <image_name>:<version>
```

We can then start this container by getting the image ID through the `docker images` command.

```dockerfile
docker start <image_ID>
```

### Building a custom image

In order to build a custom image, a blueprint file called a `Dockerfile` needs to be added to the project directory. This will contain all the configuration code, regarding what dependency versions and base image (which is the OS image that will be emulated) will be included in the container.

A typical `Dockerfile` would look somewhat similar to the one below.

```dockerfile
FROM <primary_service>:<base_image>
COPY <source code directory> /app/
WORKDIR <the working directory>
RUN <any terminal commands>
```

Now that the blueprint is made, time to build and deploy a docker container with the following configuration.

```dockerfile
docker build <location_to_save_container>
```

This builds the docker container following the blueprint, now this can be uploaded to Docker Hub or any repository to ship it to other environments and servers.