---
title: Docker Volume
description: Notes on Docker Volume.
pubDatetime: 2024-01-02T22:56:00
postSlug: docker-volume
featured: false
draft: false
tags:
  - Docker
---

![tp.web.random_picture](https://images.unsplash.com/photo-1472195870936-d88b0d4c1b41?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=300&ixid=MnwxfDB8MXxyYW5kb218MHx8dHJlZSxsYW5kc2NhcGUsd2F0ZXJ8fHx8fHwxNzA1Njc3Mzk4&ixlib=rb-4.0.3&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=900)

Notes on Docker Volume.

## Table of contents

## Introduction

When we're actively working on our codebase we certainly want our changes to reflect immediately inside our running Docker container. Rebuilding the whole image after every tiny change is not an ideal solution. There comes the Docker volumes.

![Docker Volume Representation](@assets/images/docker-volume-representation.png)

It's a process identical to port mapping but for folders/directories.

## Command

```shell
docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app {image-id}
```

Here

- `-v $(pwd):/app`: Maps the current working directory to `/app` working directory inside container.
- `-v /app/node_modules`: We signal Docker that don't try to map this directory to the local directory. Use the one that's there inside the container. See we don't have used `:` here for mapping so that will act as a placeholder.
