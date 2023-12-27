---
title: Git Aliases I Use
description: List of Git aliases that I routinely use to boost my productivity.
pubDatetime: 2023-12-25T20:31:30+05:30
postSlug: git-aliases-i-use
featured: false
draft: false
tags:
  - Git
  - Productivity
---

![tp.web.random_picture](https://images.unsplash.com/photo-1497373637916-e47a55e22d0a?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=300&ixid=MnwxfDB8MXxyYW5kb218MHx8dHJlZSxsYW5kc2NhcGUsd2F0ZXIsbW91bnRhaW58fHx8fHwxNzAzNTE3MDE2&ixlib=rb-4.0.3&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=900)

List of Git aliases that I routinely use to boost my productivity.

## Table of contents

## TLDR

Copy and run following Git alias commands in your terminal to configure on your machine!

```bash
git config --global alias.co 'checkout'
git config --global alias.cb 'checkout -b'
git config --global alias.cmt 'commit -m'
git config --global alias.cdev 'checkout dev'
git config --global alias.cmain 'checkout main'
git config --global alias.del 'branch -D'
git config --global alias.last 'log -1 HEAD'
git config --global alias.lastfiles 'log --name-only --pretty=format:"" -1'
git config --global alias.amend 'commit --amend'
git config --global alias.undo 'reset --soft HEAD^'
git config --global alias.lg '!git log --pretty=format:\"%C(magenta)%h%Creset -%C(red)%d%Creset %s %C(dim green)(%cr) [%an]\" --abbrev-commit -30'
git config --global alias.aliases '!git config -l | grep alias | sed s/^alias.//g'
```

## Introduction

I find it painful to type long Git commands for common tasks like `checkout` , `commit -m`, `checkout dev`, `reset --soft HEAD^` etc. Also, I barely remember any complex commands which forces me to Google them again and again.

I have configured following Git aliases on my machine to overcome this issue and save countless keystrokes over the time.

## List of Git Aliases

### `co`

Shortcut for `git checkout`.

```bash
git config --global alias.co 'checkout'
```

### `cb`

Shortcut for `git checkout -b` for creating a new branch and switching to it.

```bash
git config --global alias.cb 'checkout -b'
```

### `cmt`

Shortcut for `git commit -m`. Allows you to commit changes with a message in one step.

```bash
git config --global alias.cmt 'commit -m'
```

### `cdev`

Shortcut for `git checkout dev` for quickly switching to the `dev` branch.

```bash
git config --global alias.cdev 'checkout dev'
```

### `cmain`

Shortcut for `git checkout main` for quickly switching to the `main` branch.

```bash
git config --global alias.cmain 'checkout main'
```

### `del`

Shortcut for `git branch -D` to force delete a branch.

```bash
git config --global alias.del 'branch -D'
```

### `last`

Displays the last commit, useful for a quick look at the latest changes.

```bash
git config --global alias.last 'log -1 HEAD'
```

### `lastfiles`

Shortcut to fetch the list of affected files in your last commit.

```bash
git config --global alias.lastfiles 'log --name-only --pretty=format:"" -1'
```

### `amend`

Amends the last commit, allowing you to add changes to the previous commit.

```bash
git config --global alias.amend 'commit --amend'
```

### `undo`

Undoes the last commit but leaves changes staged.

```bash
git config --global alias.undo 'reset --soft HEAD^'
```

### `lg`

Custom log format to display a concise and colourful log.

```bash
git config --global alias.lg '!git log --pretty=format:\"%C(magenta)%h%Creset -%C(red)%d%Creset %s %C(dim green)(%cr) [%an]\" --abbrev-commit -30'
```

### `aliases`

Lists all Git aliases you have configured. My favourite! 😉

```bash
git config --global alias.aliases '!git config -l | grep alias | sed s/^alias.//g'
```
