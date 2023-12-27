---
title: Docker Commands
description: List of core Docker commands you must know.
pubDatetime: 2020-05-20T00:00:00
postSlug: docker-commands
featured: false
draft: false
tags:
  - Docker
  - DevOps
---

![tp.web.random_picture](https://images.unsplash.com/photo-1605745341112-85968b19335b?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=300&ixid=MnwxfDB8MXxyYW5kb218MHx8dHJlZSxsYW5kc2NhcGUsd2F0ZXIsbW91bnRhaW58fHx8fHwxNzAzNzA2MDcx&ixlib=rb-4.0.3&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=900)

List of core Docker commands you must know.

## Table of contents

## Pull

```bash
# pulls `latest` Docker image of nginx
docker pull nginx

# pulls version 1.23 image of nginx
docker pull nginx:1.23
```

## List Images

```bash
docker images
```

## Create a container

```shell
docker create {image-name}
```

## Run a container

- The `start` command starts one or more stopped containers.

```shell
docker start {container-id}
```

- Docker `run` command creates a new container everytime. It doesn't reuse previous container.
- `docker run` = `docker create` + `docker start`

```shell
docker run {name}:{tag}

# Runs a container in the background
docker run -d nginx:1.23
```

## Container Naming

- Docker auto-generates unique random names for each container instance.
- We can set more meaningful container names manually.

```shell
docker run --name web-app -d -p 9000:80 nginx:1.23
```

## Stop a container(s)

```shell
# stops the container by container id
docker stop {container-id}
```

```shell
# stops the contianer by container name
docker stop {container-name}
```

```shell
# stops multiple container having id and/or name
docker stop {container-id} {container-name}
```

## List containers

```shell
# Lists all running containers
docker ps
```

```shell
# List all containers either running or stopped
docker ps -a
```

## View logs from a running container

```shell
docker logs {container-id}
```

## Port binding

```shell
# Use -p or --publish option for port binding.
# Here,
# HOST_PORT -> 9000
# CONTAINER_PORT -> 80
docker run -d -p 9000:80 nginx:1.23
```

## Build an image

```shell
# -t or --tag
docker build -t node-app:1.0 .
```

## References

- [Udemy: Docker & Kubernetes - The Complete Guide](https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/)
- [Docker Crash Course by TechWorld with Nana](https://www.youtube.com/watch?v=pg19Z8LL06w)
