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

#### Codebase

* Always tracked in a version control system.
* A codebase is any single repo, or any set of repos who share a root commit.
* There is always one-to-one correlation b/w the codebase and the app.
* Multiple codebases are distributed systems not an app.
* Mutliple apps can not share code. Use/create libraries as a solution.
* Use dependency manager.
* Only one codebase per app, but many depolys of the app. A deploy is running instance of the app. For example, production sites, staging sites, dev1 site can be called deploys.

#### Dependencies

* A twelve-factor app never relies on implicit existence of system-wide packages/system tools like *ImageMagick* or *curl*.
* Explicit declaration of dependencies benefits new developers in setting up the app.

#### Config

Store config in the environment

* app's *config* is everything that can vary between deploys like Resource handles, Keys to third party services, per-deploy values such as hostname.
* storing config in the form of *Constant* in the code is a violation in TFA.
* advocates **strict separation of config from code**.
* codebase should be open-sourced at any point of time without compromising any credentials.
* The TFA stores config in environment variables.
* Env vars are easy to change b/w deploys, little chance of getting pushed to repo accidently.

#### Backing services

Treat backing services as attached resources

> A backing service is any service the app consumes over the network as part of its normal operation. Examples include datastores (such as MySQL or CouchDB), messaging/queueing systems (such as RabbitMQ or Beanstalkd), SMTP services for outbound email (such as Postfix), and caching systems (such as Memcached).

* The code for a twelve-factor app makes no distinction between local and third party services.
* A deploy of the twelve-factor app should be able to swap out a local service with one managed by a third party without any changes to the app’s code.
* Each distinct backing service is a resource.

> Resources can be attached and detached to deploys at will. For example, if the app’s database is misbehaving due to a hardware issue, the app’s administrator might spin up a new database server restored from a recent backup. The current production database could be detached, and the new database attached – all without any code changes.

#### Build, release, run

Strictly separate build and run stages

* A codebase is transformed into a (non-development) deploy through three stages: The *build stage*, The *release stage*, and The *run stage*.
* Every release should always have a unique release ID.
* Any change must create a new release.

#### Processes

Execute the app as one or more stateless processes

* Twelve-factor processes are stateless and share-nothing. Any data that needs to persist must be stored in a stateful backing service, typically a database.
* The twelve-factor app never assumes that anything cached in memory or on disk will be available on a future request or job.
* Sticky sessions are a violation of twelve-factor and should never be used or relied upon. Session state data is a good candidate for a datastore that offers time-expiration, such as Memcached or Redis.

#### Port binding

Export services via port binding

The [official document's explanation](https://12factor.net/port-binding) is unclear.  However, following excerpt from [stackoverflow question](https://stackoverflow.com/q/26491425) is a bit of help.

> Port binding exists to solve the problem of "port brokering" at the platform level. If every application worker listened on port 80 there would be conflicts. To solve this, port binding is a convention whereby the application listens on a port the platform has allocated -- and which is passed in as a $PORT environment variable. This ensures a) the application worker listens on the right port and b) the platform knows where to route traffic destined for that worker. [answer link](https://stackoverflow.com/a/27140353)

Another good read on Port Binding https://jiraaya.wordpress.com/2014/05/16/twelve-factor-port-binding.

#### Concurrency

Scale out via the process model

* In the twelve-factor app, processes are a first class citizen.
* Twelve-factor app processes should never daemonize or write PID files.

#### Disposability

Maximize robustness with fast startup and graceful shutdown

* Disposability means app's processes can be started or stopped really fast. It helps in rapid scaling and depolyment of code or config changes.
* Processes shut down gracefully when they receive a **SIGTERM** signal.
* Web process can achieve graceful shutdown by ceasing to listen on the service port, allowing any current requests to finish, and then exit.
* Worker process aheives graceful shutdown by moving the current job to the work queue.

#### Dev/prod parity

Keep development, staging, and production as similar as possible

* Keep the tool stack identical across the deploys. If you deploy your application on Linux, using Windows for development is not the right choice.

* Tiny incompatibilities in Dev and Prod environment hurts the Continuous Deployment cycle over the lifetime of an application.

#### Logs

* Logs provide visibility into the behaviour of a running app.
* Logs are texts, one event per line.

#### Admin processes

* Twelve-factor strongly favors languages which provide a REPL shell out of the box.