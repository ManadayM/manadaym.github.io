---
layout: post
title: Twelve-Factor App Notes
---

I found a new terminology or a methodology called Twelve Factor App while reading an article about [The Process Module of Node.js](https://blog.risingstack.com/mastering-the-node-js-core-modules-the-process-module/). This post is a selfnote on the same. Throughtout this post TFA is used as an acronym for Twelve-Factor App.

<!--more-->

The twelve-factor app is a methodology for building software-as-a-service apps that:

* Use declarative formats for setup automation, to minimize time and cost for new developers joining the project;
* Have a clean contract with the underlying operating system, offering maximum portability between execution environments;
* Are suitable for deployment on modern cloud platforms, obviating the need for servers and systems administration;
* Minimize divergence between development and production, enabling continuous deployment for maximum agility;
* And can scale up without significant changes to tooling, architecture, or development practices.

The twelve-factor methodology can be applied to apps written in any programming language, and which use any combination of backing services (database, queue, memory cache, etc).

## The Twelve Factors

**Codebase**
    - Always tracked in a version control system
    - A codebase is any single repo, or any set of repos who share a root commit
    - There is always one-to-one correlation b/w the codebase and the app
    - Multiple codebases are distributed systems not an app
    - Mutliple apps can not share code. Use/create libraries as a solution.
    - Use dependency manager

**Dependencies**
**Config**
**Backing services**
**Build, release, run**
**Processes**
**Port binding**
**Concurrency**
**Disposability**
**Dev/prod parity**
**Logs**
**Admin processes**
