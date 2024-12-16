---
title: Connect MongoDB on Windows from WSL2
description: A quick guide to connect MongoDB on Windows from WSL2.
pubDatetime: 2024-12-16T21:33:00
postSlug: connect-mongodb-on-windows-from-wsl2
featured: false
draft: false
tags:
  - MongoDB
  - Windows
  - WSL
---

![tp.web.random_picture](https://images.unsplash.com/photo-1517842645767-c639042777db?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=300&ixid=MnwxfDB8MXxyYW5kb218MHx8dHJlZSxsYW5kc2NhcGUsd2F0ZXJ8fHx8fHwxNzA1Njc0NDkx&ixlib=rb-4.0.3&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=900)

Quick guide to connect MongoDB on Windows from WSL2.

## Table of contents

## Introduction

Recently, I encountered an issue connecting to MongoDB running on Windows from WSL2 (Windows Subsystem for Linux). Being new to the Windows and WSL ecosystem after using Apple machines for 15 years, I spent about 4 hours troubleshooting. After diving through various online threads, I managed to resolve the issue using the following steps.

## Steps

#### Stop the `MongoDB` Service
- Stop the `MongoDB` service from Windows `Services`.

#### Locate MongoDB configuration file
- Locate `mongod.cfg` config file using `File Explorer`. 

Typically it's found at `C:\Program Files\MongoDB\Server\8.0\bin`. Replace `8.0` with your installed MongoDB version.

#### Edit `mongod.cfg` file
- Open command prompt with `Administrator` privilages and `cd` into the directory where `mongod.cfg` file is located.
- Run `notepad mongod.cfg` to open file in Notepad.
- Update `bindIp` parameter from

```
 bindIp: 127.0.0.1
```
 to 
 ```
 bindIp: 0.0.0.0
 ```

#### Allow MongoDB through Windows Firewall
- Search for `Allow an app through Windows Firewall` in the Windows search bar.
- Click `Change settings` on top right corner.
- Click `Allow another app...` button at the bottom right.
- Click `Browse` to locate and select the `mongod.exe`.
- Click `Network types` and ensure both `private` and `public` network types are selected.
- Click `Add` to create a set of inbound rules for MongoDB in the Windows Defender Firewall.

#### Restart the MongoDB service
- Go back to `Services` and start the `MongoDB` service.

#### Find your Windows host IPv4 address
- Run `ipconfig` command in your command prompt.
- Note the IPv4 address under the active network adapter (e.g., 192.168.x.x)

#### Update MongoDB URI in WSL2
- Use the noted IPv4 address to modify your MongoDB connection URI in WSL2. For example

```
mongodb://<your-host-ipv4-address>:27017/<your-db-name>
```

## Conclusion

By following these steps, I successfully connected to a local MongoDB instance running on Windows from my Serverless API project running inside WSL2. 🎉

