---
layout: post
title: Twelve-Factor App Notes
---

I found a new terminology or a methodology called Twelve Factor App while reading an article about [The Process Module of Node.js](https://blog.risingstack.com/mastering-the-node-js-core-modules-the-process-module/). This post is a selfnote on the same.

<!--more-->

The twelve-factor app is a methodology for building software-as-a-service apps that:

* Use **declarative** formats for setup automation, to minimize time and cost for new developers joining the project;
* Have a **clean contract** with the underlying operating system, offering **maximum portability** between execution environments;
* Are suitable for **deployment** on modern **cloud platforms**, obviating the need for servers and systems administration;
* **Minimize divergence** between development and production, enabling **continuous deployment** for maximum agility;
* And can **scale up** without significant changes to tooling, architecture, or development practices.

The twelve-factor methodology can be applied to apps written in any programming language, and which use any combination of backing services (database, queue, memory cache, etc).

## The Twelve Factors

**Codebase**
* Always tracked in a version control system.
* A codebase is any single repo, or any set of repos who share a root commit.
* There is always one-to-one correlation b/w the codebase and the app.
* Multiple codebases are distributed systems not an app.
* Mutliple apps can not share code. Use/create libraries as a solution.
* Use dependency manager.
* Only one codebase per app, but many depolys of the app. A deploy is running instance of the app. For example, production sites, staging sites, dev1 site can be called deploys.

**Dependencies**
* A twelve-factor app never relies on implicit existence of system-wide packages/system tools like *ImageMagick* or *curl*.
* Explicit declaration of dependencies benefits new developers in setting up the app.

**Config**
Store config in the environment
* app's *config* is everything that can vary between deploys like Resource handles, Keys to third party services, per-deploy values such as hostname.
* storing config in the form of *Constant* in the code is a violation in TFA.
* advocates **strict separation of config from code**.
* codebase should be open-sourced at any point of time without compromising any credentials.
* The TFA stores config in environment variables.
* Env vars are easy to change b/w deploys, little chance of getting pushed to repo accidently.

**Backing services**
Treat backing services as attached resources
> A backing service is any service the app consumes over the network as part of its normal operation. Examples include datastores (such as MySQL or CouchDB), messaging/queueing systems (such as RabbitMQ or Beanstalkd), SMTP services for outbound email (such as Postfix), and caching systems (such as Memcached).
* The code for a twelve-factor app makes no distinction between local and third party services.
* A deploy of the twelve-factor app should be able to swap out a local service with one managed by a third party without any changes to the app’s code.
* Each distinct backing service is a resource.

> Resources can be attached and detached to deploys at will. For example, if the app’s database is misbehaving due to a hardware issue, the app’s administrator might spin up a new database server restored from a recent backup. The current production database could be detached, and the new database attached – all without any code changes.

**Build, release, run**
Strictly separate build and run stages

* A codebase is transformed into a (non-development) deploy through three stages: The *build stage*, The *release stage*, and The *run stage*.
* 

**Processes**
**Port binding**
**Concurrency**
**Disposability**
**Dev/prod parity**
**Logs**
**Admin processes**
