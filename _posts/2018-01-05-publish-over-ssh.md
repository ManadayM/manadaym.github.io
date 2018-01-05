---
layout: post
title: Publish Over SSH
---
How I published build artifacts to remote machine from Jenkins server?
<!--more-->

## Background
I successfully implemented Continuous Integration and Continuous Deployment through Jenkins on our Dev Server. On the Dev server, twice a day, Jenkins pulls develop branch from bitbucket and builds the project. It also takes backup of current live website's artifacts before publishing the new one. This process completely removed the requirement of manual deployment twice a day.

We decided to take this process to the Staging environment. However, this time the challenging part was to use a specific Jenkins server as a build server and deploy the build artifacts over the staging server, which is a completely different AWS instance.

A little bit Googling brought me two options for the problem.

1. [Publish Over SSH](https://wiki.jenkins.io/display/JENKINS/Publish+Over+SSH+Plugin)
2. [Master Slave concept](https://wiki.jenkins.io/display/JENKINS/Distributed+builds)

I tried both the ways and faced different set of problems. This document will cover how I achieved the goal using first approach.

### Step-by-step guide

#### On Remote Machine

Install [SSH server](http://www.freesshd.com/index.php?ctt=download) on remote machine and make sure *Port 22* is enabled. Here is a good [how to guide to set up SSH server FreeSSHD](http://johnklann.com/how-to-setup-a-ssh-server-on-windows/). Ignore Step 3 in the guide.

At this stage you should be up and running with SSH server having at least one user added with windows logon credentials as mentioned in the how to guide in the previous step.

Add a central directory where all file transfers (build artifacts) from jenkins machine will be kept. Go to *FreeSSHD > SFTP tab > SFTP home path* and set the field to your desired directory.

![SFTP Home Path]({{ site.url }}public/images/2018-01-05-publish-over-ssh/sftp-home-path.png)

#### On Jenkins Machine

Install Publish Over SSH plugin on Jenkins. Installing the plugin will add its configuration entry inside System Configuration.

Go to *Manage Jenkins > Configure System > Search **Publish over SSH***

Leave the **Jenkins SSH Key** section empty unless you want to authenticate and establish SSH connection using SSH Keys. In our case, we used RDP credentials for the authentication.

You can add multiple remote servers under **SSH Servers** section. For now, **Add** your remote machine (here UAT Server) credentials like shown in the screenshot.

![Add SSH Server]({{ site.url }}public/images/2018-01-05-publish-over-ssh/add-ssh-server.png)

Check if configuration done so far on the UAT Server and Jenkins are done right or not using **Test Configuration** button. If all steps done right, you will see **Success** message.

Hit **Save** button.

#### Inside Jenkins Job

You can use Publish over SSH plugin inside Jenkins job at multiple levels like before build starts, after build completes or under *Post-Build Actions* section as **Send build artifacts over SSH**. Since we wanted to push build artifacts upon completion of build process. We chose to add transfer process under *Post-Build Actions* section.

Select **Send build artifacts over SSH** under **Post-Build Actions** section.

Select your remote machine from the dropdown where you wish to push the build stuff.

Under **Transfer Set**

* **Source Files** - add relative path to the build directory where build artifacts reside.
* **Remove Prefix** - First part of the file path that should not be created on the remote server.
* **Remote Directory** - Destination folder where all these stuff should be placed. The directory name mentioned here will be created under your SFTP home path configured on your SSH server.

![Transfer Set]({{ site.url }}public/images/2018-01-05-publish-over-ssh/transfer-set.png)

In our case we wanted to take back up of existing stuff on remote server before pushing the new stuff. For this you can use **Exec command** although this command executes after file transfer happens. To make this command execute first, Add new transfer set and move it to top in the Transfers stack.

Exec command is different from normal Windows batch command. [You cannot execute more than one command there](https://issues.jenkins-ci.org/browse/JENKINS-17809).

![For Backup]({{ site.url }}public/images/2018-01-05-publish-over-ssh/exec-command.png)

The command highlighted here will copy/backup current website copy to *D:\Manaday\yyyymmdd* folder.

This is it. If all goes right your build package will be transferred to the remote server. And jenkins job will show SUCCESS status at the end.