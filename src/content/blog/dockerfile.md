---
title: Dockerfile
description: Dockerfile 101.
pubDatetime: 2020-05-25T00:00:00
postSlug: dockerfile
featured: false
draft: false
tags:
  - Docker
  - DevOps
---

![tp.web.random_picture](https://images.unsplash.com/photo-1605745341112-85968b19335b?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=300&ixid=MnwxfDB8MXxyYW5kb218MHx8dHJlZSxsYW5kc2NhcGUsd2F0ZXIsbW91bnRhaW58fHx8fHwxNzAzNzA2MDcx&ixlib=rb-4.0.3&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=900)

Dockerfile 101.

- Companies create custom images for their applications.
- `Dockerfile` is a **text document** having commands to create an image.
- Dockerfiles start from a parent image or **base image**. Such base images are mostly lightweight Linux OS image that has node, npm or whatever tool you need for your application on top of it.
- Every image consists of multiple image layers. This makes Docker very efficient as image layers can be cached.
- **REMEMBER:** Each instruction in the `Dockerfile` creates one layer. These layers are stacked & each one is a delta of the changes from the previous layer.

```dockerfile
# Base image
FROM node:19-alpine

# Copies package.json from host to docker env.
# The "/" at the end ensures directory creation at the Linux root (front "/")
COPY package.json /app/

COPY src /app/

# WORKDIR sets the working directory for all following commands.
WORKDIR /app

# Runs this command in a shell inside the container environment
RUN npm install

# The instruction that is to be executed when a Docker container starts
# There can be only on "CMD" instruction in a Dockerfile.
CMD ["node", "server.js"]
```

## Build an image

```shell
# -t or --tag
docker build -t node-app:1.0 .
```

## References

- [Udemy: Docker & Kubernetes - The Complete Guide](https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/)
- [Docker Crash Course by TechWorld with Nana](https://www.youtube.com/watch?v=pg19Z8LL06w)
