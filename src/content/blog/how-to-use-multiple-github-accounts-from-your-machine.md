---
title: Use multiple Github accounts from your machine
description: Guide to operate multiple Github accounts on your machine.
pubDatetime: 2024-05-29T00:20:48
postSlug: how-to-use-multiple-github-accounts-from-your-machine
featured: false
draft: false
tags:
  - Git
  - Productivity
---

![tp.web.random_picture](https://images.unsplash.com/photo-1618401471353-b98afee0b2eb?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=300&ixid=MnwxfDB8MXxyYW5kb218MHx8bGFuZHNjYXBlLHdhdGVyLG1vdW50YWlufHx8fHx8MTY2MTU3NjExNA&ixlib=rb-1.2.1&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=900)

A guide on how to operate multiple Github accounts from your machine.

## Table of contents

## Overview

As a freelancer I have to work with multiple Github accounts that belong to different clients of mine. Typing password at each git push or pull is a wastage of time. It is also painful to remember credentials for multiple accounts.

## Solution

You can access and write data in repositories on GitHub.com using SSH (Secure Shell Protocol). I know that's something common we all know. However, we can define the host aliases in our ssh config file for each account.

### Steps

1. You must have [generated ssh key pairs for accounts](https://help.github.com/articles/generating-a-new-ssh-key/) and then [have added them to Github accounts](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/).
2. Edit or create ssh config file at `~/.ssh/config`.

```shell
# Primary (Default) github account: ManadayM
Host github.com
	Hostname github.com
	IdentityFile ~/.ssh/manadaym_private_key
	IdentitiesOnly yes

# Secondary github account: clientname
Host github-clientname
	Hostname github.com
	IdentityFile ~/.ssh/client_private_key
	IdentitiesOnly yes
```

3. [Add your SSH keys to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent)

```shell
$ ssh-add ~/.ssh/manadaym_private_key
$ ssh-add ~/.ssh/client_private_key
```

4. Test your connection

```shell
# Fetches the public SSH keys from github.com and appends them to the local known_hosts file.
$ ssh-keyscan github.com >> ~/.ssh/known_hosts

# Tests the SSH connections.
$ ssh -T git@github.com
$ ssh -T git@github-clientname
```

By now you should see the following messages.

```
Hi ManadayM! You've successfully authenticated, but GitHub does not provide shell access.
```

```
Hi ClientName! You've successfully authenticated, but GitHub does not provide shell access.
```

5. You're all set!

```
git@github-clientname:clientname/project.git => user is clientname
git@github.com:ManadayM/project.git.     => user is ManadayM
```

- Clone a repository

```shell
$ git clone git@github-clientname:clientname/project1.git /path/to/project1
$ cd /path/to/project1
$ git config user.email "manaday@client.com"
$ git config user.name  "Manaday Mavani"
```

- Change the `origin` URL for the existing repository.

```shell
$ cd /path/to/project2
$ git remote set-url origin git@github-clientname:clientname/project2.git
$ git config user.email "manaday@client.com"
$ git config user.name  "Manaday Mavani"
```

That's all folks!

PS - While I'm using this idea since long, I decided to document the steps for my future reference. A quick Googling on this topic brought me to the referenced [gist by oanhnn](https://gist.github.com/oanhnn/80a89405ab9023894df7). I have borrowed/copied many parts of his gist for this note. Hence, all credit goes to him for the writeup. 🙏🏼😅

## References

- [Step by step guide by oanhnn](https://gist.github.com/oanhnn/80a89405ab9023894df7)
