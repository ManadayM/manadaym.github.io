---
title: Docker Overview
description: My notes on Docker taken from multiple sources over the time.
pubDatetime: 2020-05-11T20:11:10+05:30
postSlug: docker-overview
featured: false
draft: false
tags:
  - Docker
  - DevOps
---

![tp.web.random_picture](https://images.unsplash.com/photo-1605745341112-85968b19335b?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=300&ixid=MnwxfDB8MXxyYW5kb218MHx8dHJlZSxsYW5kc2NhcGUsd2F0ZXIsbW91bnRhaW58fHx8fHwxNzAzNzA2MDcx&ixlib=rb-4.0.3&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=900)

My notes on Docker taken from multiple sources over the time.

## Table of contents

## What is Docker?

- Docker is a virtualisation software.
- Makes developing and deploying applications much easier.
- Packages application with all necessary dependencies, configuration, system tools and runtime.

## What problems solve Docker?

- Without containers

  - Each developer needs to install and configure all services directly on their OS on their local machine.
  - Installation process different for each OS env.
  - Many steps, were something can go wrong.
  - If you've 10 services then each developer need to install 10 those services.

- With containers
  - With containers you won't need to install any of the services directly on your OS.
  - Start service as a Docker container using a single Docker command.
  - Same command for all OS.
  - Docker standardises process of running any service on any local dev environment.
  - Easy to run different version of the same app without any conflicts.

## Virtual Machine vs Docker

- OS has 2 main layers - OS Kernel, OS Applications Layer.
- Kernel layer communicates with the hardware components.
- **Docker virtualises the applications layer. It uses the kernel of the host.**
- **Virtual Machine has the applications layer and its own kernel. It virtualises the complete OS.**
- Size of the Docker images are much smaller as they just have to implement one layer of the OS.
- Containers take seconds to start as compared to VMs which usually take minutes.
- VMs works on all OS. Docker was originally built for Linux distros. However, using Docker Desktop we can run Docker containers on Windows and MacOS. Docker Desktop uses **Hypervisor layer** with a _lightweight_ Linux distribution in it to provide needed Linux kernel.

## Docker Images vs Containers

- Docker allows to package the application with its environment config in package that you can share easily. Think of it like a zip or tar-file which you can upload to your Artifact Repository and then download on your server whenever you needed. This package is known as Docker Image.
- Docker Image still differs from traditional application artifacts as it contains app source code and environment configuration.
- A running instance of Docker Image is a Docker Container.
- You can run multiple containers from 1 image.

## Docker Registries

- A storage and distribution system for Docker images. Think of it as npm which is a package registry for Node.js modules.
- Official images available from applications like [Redis](https://hub.docker.com/_/redis), [PostgreSQL](https://hub.docker.com/_/postgres), and [MongoDB](https://hub.docker.com/_/mongo).
- Docker hosts one of the biggest Docker Registry, called [Docker Hub](https://hub.docker.com/).
- **Docker Hub is the default registry in Docker.**
- A dedicated team at Docker is responsible for reviewing and publishing all content in the Docker Official Images.

## Docker Image Versions

- Images are versioned as technology changes. Each different versions are identified by **tags**.
- There is a special tag that all images have called **latest**. If you don't specify the version then you get the latest versioned image.
- **Using a specific version is the best practice in most cases.**

## Port Binding

- Application inside container runs in an **isolated Docker network**.
- This allows us to run the same app running on the same port multiple times.
- We need to expose the container port to the host (the machine container runs on) to make the service available to the outside world.
- Port binding flow: `-p {HOST_PORT}:{CONTAINER_PORT}`.
- Only 1 service can run on a specific port on the host.
- Although, you can use any port number on your host but industry standard is to use the same port on your host as container is using.

![Docker Port Binding](@assets/images/docker-port-binding.png)

## Public and Private Docker Registries

- There are two types of registries - **public** and **private**.
- Docker Hub is the largest **public** registry.
- All big cloud providers offer private registries - AWS ECR, Google Container Registry, etc.
- Docker Hub also provides private registry.

## Registry vs Repository

- Registry is a service providing storage.
- Can be hosted by a third party, like AWS, or by yourself.
- Inside that registry, you can have collection of repositories **having related images** with same name but different versions.

## References

- [Udemy: Docker & Kubernetes - The Complete Guide](https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/)
- [Docker Crash Course by TechWorld with Nana](https://www.youtube.com/watch?v=pg19Z8LL06w)
