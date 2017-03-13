---
start: true
title: "Containers"
teaching: 60
exercises: 0
questions:
- "What is a software container?"
- "What's Docker? What's Singularity? And what is each good for?"
- "How do I run software in a container?"
- "How do I build a container?"
- "What are some best practices to ensure reproducibility and ease of use?"
- "How do I use containers that are publicly available on Docker Hub and Singularity Hub?"
- "Where can I go to learn more?"
objectives:
- "List key aspects of software containers, how they differ from virtual machines, and give a few examples of popular software."
- "Describe basics steps of building and using containers."
- "Understand that containers can be shared easily on Docker Hub and Singularity Hub just as code is shared on GitHub."
- "Know where to go to get more information."
keypoints:
- "Containers allow applications to run in a self-contained, reproducible environment."
- "Containers can be copied and shared allowing you to replicate your results on a new machine, or colleagues to replicate your results in a different environment."
- "Individuals and organizations distribute software in containers on Docker Hub and Singularity Hub."
- "You can learn more about containers at [Docker Home](https://docs.docker.com/), [Singularity Home](http://singularity.lbl.gov/), and [Singularity at the NIH HPC](https://hpc.nih.gov/apps/singularity.html)."
---

# What's a software container? (And what's it good for?)
Software containers allow you to package an application along with all of its dependencies in a portable, shareable format. Containers package <b>ALL</b> of an apps dependencies... including an entire operating system!  This ensures reproducibility across different computers and environments.  

Containers allow you to do things like:
* Package an analysis pipeline so that it runs on your laptop, in the cloud, and in a high performance computing (HPC) environment to produce the same result.
* Publish all of the software and data from a project along with the paper so that others can reproduce your results.
* Install and run an application that requires a complicated software stack on a new computer with a few keystrokes.

## Containers vs. Virtual Machines
Containers are a type of virtualization and they are related to virtual machines (VMs). But there are a few important differences between the two. A VM has it's own kernel.  This allows the VM to directly access to the hardware and it allows for more flexibility. For instance, you can run a Linux VM on Windows or on a Mac. In contrast containers share a kernel with the host system.  This makes containers less flexible (a Linux host can typically only support Linux containers), but it also makes them *much* faster.  Because of these differences, VMs and containers are useful in different scenarios. If want to interact with your computer using a different operating system, you should usually install a VM.  But if you just need to run one or two apps in a different environment containers are a better choice. 

## Docker   
The most popular and widely used container software is [Docker](https://docs.docker.com/).  Docker is a very mature program with a large user community.  [Docker Hub](https://hub.docker.com/) gives Docker users a place to build and host their containers.  It's fully integrated into the core Docker program, allowing you to download any of over 100,000 pre-built containers from the command prompt.  This arrangement produces a ecosystem in which containers can be easily orchestrated.

Docker is extremely powerful, but it is also a bit difficult to learn.  At first, some of it's inner workings may seem hidden.  For instance, after downloading a container, it may not be immediately clear where that container resides or how it is represented on the local computer.  And Docker is not well-suited for HPC environments where a large number of users share the same storage and operating system.  Still, with its powerful feature set and ecosystem Docker is often the best choice for a new project.

## Singularity
Singularity is a very new program that is still under active development. It is relative easy to use, and it is well-suited for HPC environments. Docker containers can be converted for use with Singularity and current versions of Singularity can import containers directly from Docker Hub. Containers can also be imported from [Singularity Hub](https://singularity-hub.org/).

The philosophy of Singularity differs somewhat from that of Docker.  Docker basically assumes that you will build (or download) and run your containers on the same system, and that you will be a root (administrative) user on that system.  Singularity assumes that you will build your containers on a system where you have root access, run your containers may run in an environment where you are an unprivileged user. So the singularity philosophy assumes you will have a *build system* (a Linux laptop, VM, or cloud instance) where you have root access, but this may differ from your *production system* where you run your containers and may or may not have root privileges.   

We will use Singularity for the demonstration below.  

## Getting more information about containers
This demo will only give you a brief taste of software containers. If you want to learn more, the following websites will give you a good place to start:
* [Docker Home](https://docs.docker.com/)
* [Singularity Home](http://singularity.lbl.gov/)
* [Singularity at the NIH HPC](https://hpc.nih.gov/apps/singularity.html)

# Introduction to Singularity
To start with, let's say that you are using a Linux computer with Ubuntu 16.04.

~~~
$ cat /etc/os-release
~~~
{: .bash}

~~~
NAME="Ubuntu"
VERSION="16.04.2 LTS (Xenial Xerus)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 16.04.2 LTS"
VERSION_ID="16.04"
HOME_URL="http://www.ubuntu.com/"
SUPPORT_URL="http://help.ubuntu.com/"
BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"
VERSION_CODENAME=xenial
UBUNTU_CODENAME=xenial
~~~
{: .output}

And let's also assume that you already have a Singularity container image.  We'll say it's called `centos.img`.  

~~~
$ pwd
~~~
{: .bash}

~~~
/home/ubuntu
~~~
{: .output}

~~~
$ ls
~~~
{: .bash}

~~~
centos.img  singularity
~~~
{: .output}

You can see that I also have a directory called `singularity`.  That contains the source code for Singularity that I downloaded from github.  More on that later.  

The simplest way to use this container would be to just start an interactive shell inside.  Singularity allows you to do this with the `shell` command.

~~~
$ singularity shell centos.img
~~~
{: .bash}

~~~
Singularity: Invoking an interactive shell within container...

Singularity.centos.img>
~~~
{: .output}

Notice that the command prompt changed from a dollar sign to a longer string.  This is because the default shell in ubuntu is `/bin/bash`, but the default shell in a Singularity container is `/bin/sh`.  (Some containers may not have `/bin/bash` installed.)  Anyway, let's check the information about our operating system again.

~~~
Singularity.centos.img> cat /etc/os-release
~~~
{: .bash}

~~~
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"
~~~
{: .output}

The contents of `/etc/os-release` are totally different when viewed from inside the container.  In fact, the entire operating system has been swapped with a new one (including the GNU C and C++ libraries, the core utilities, and any installed binary executables). But even though most things about our new environment have changed, some things remain the same.  Let's see what our home directory looks like.

~~~
Singularity.centos.img> pwd
~~~
{: .bash}

~~~
/home/ubuntu
~~~
{: .output}

~~~
Singularity.centos.img> ls
~~~
{: .bash}

~~~
centos.img  singularity
~~~
{: .output}

The home directory on our host system is still visible from within the Singularity container.  What happens if we try to write to this directory?

~~~
Singularity.centos.img> echo foo > ~/bar 
Singularity.centos.img> ls
~~~
{: .bash}

~~~
bar   centos.img
~~~
{: .output}

~~~
Singularity.centos.img> cat bar 
~~~
{: .bash}

~~~
foo
~~~
{: .output}

Looks like we can write to our home directory from within the container.  What happens to this new file once we exit the Singularity container?

~~~
Singularity.centos.img> exit
$ ls
~~~
{: .bash}

~~~
bar   centos.img    singularity
~~~
{: .output}

~~~
$ cat bar 
~~~
{: .bash}

~~~
foo
~~~
{: .output}

You may have expected `bar` to disappear once we exited the container, but you can see that it remained.

So in summary, we were able to write the text `foo` to a file `bar` in our home directory from within the container and these changes persisted on the host system even after we exited the container.  This is because Singularity *binds* a user's home directory into the container when it is initiated.  Singularity blurs the lines between a container and the host system by binding several directories to a container when it initiated.  These include `/home/$USER`, `$PWD`, `/tmp`, `/proc`, `/sys` and a few others.  This convenient feature allows you to install a program to perform some analysis within a container, and then use it to read, analyze, and write data to the host system.  

If the default directories don't suit your needs, you can customize which directories Singularity binds into you container.  For instance, if you wanted to read from and write to a directory called `/data` you could bind that directory to your container using the `--bind` argument.  See the documentation at [Singularity Home](http://singularity.lbl.gov/), or [Singularity at the NIH HPC](https://hpc.nih.gov/apps/singularity.html) for more details on this procedure.

# Creating your own Singularity containers
As noted in the introduction, you must have root (administrative) rights on a Linux system to create build and manage Singularity containers.  Once your container is built, you can move it to an environment where you don't have root access (like an HPC system) and run it there.  

Creating a Singularity container is a two-step process.  First, you must create an empty container image with the `singularity create` command.  Then you must install an operating system and any apps you want to run with the `singularity bootstrap` command.

Let's create an empty container and install Ubuntu.

~~~
$ sudo singularity create ubutnu.img 
~~~
{: .bash}

~~~
Creating a new image with a maximum size of 768MiB...
Executing image create helper
Formatting image with ext3 file system
Done.
~~~
{: .output}

~~~
$ ls 
~~~
{: .bash}

~~~
bar     centos.img  ubuntu.img  singularity
~~~
{: .output}

Now we must execute `singularity bootstrap` to install an operating system into the empty image.  The `bootstrap` command requires a *definition file*, which is like a set of blueprints detailing how the container should be built.  You may recall that I have a sub-directory called `singularity` in my home directory.  It contains another sub-directory called `examples` with example definition files. 

~~~
$ ls ~/singularity/examples
~~~
{: .bash}

~~~
arch.def  busybox.def  centos.def  contrib  debian.def  docker.def  legacy  README  scientific.def  ubuntu.def
~~~
{: .output}

Let's copy the ubuntu.def to our working directory and examine it's contents.

~~~
$ cp ~/singularity/examples/ubuntu.def .
$ cat ./ubuntu.def
~~~
{: .bash}

~~~
# Copyright (c) 2015-2016, Gregory M. Kurtzer. All rights reserved.
#
# "Singularity" Copyright (c) 2016, The Regents of the University of California,
# through Lawrence Berkeley National Laboratory (subject to receipt of any
# required approvals from the U.S. Dept. of Energy).  All rights reserved.

BootStrap: debootstrap
OSVersion: trusty
MirrorURL: http://us.archive.ubuntu.com/ubuntu/


%runscript
    echo "This is what happens when you run the container..."


%post
    echo "Hello from inside the container"
    sed -i 's/$/ universe/' /etc/apt/sources.list
    apt-get -y install vim

~~~
{: .output}

Beneath the copyright information there are several sections.  The first section, the Header, has several keywords (`Bootstrap`, `OSVersion`, and `MirrorURL`) which give Singularity information about how to create the OS, which version to use, and from where to download it.  The `%runscript` section tells Singularity what this container should do when it is called without any other input.  In this case it will just echo a short message to standard output.  The `%post` section is used to customize your container.  It tells Singularity what commands should run in the container after the OS is installed.  In this case Singularity will echo a "Hello" message, use use the stream editor `sed` to edit a configuration file, and then use the `apt` package manager to install a text editor (`vim`).
* Basics
* Advanced techniques

# Using pre-built containers from [Docker Hub](https://hub.docker.com/) and [Singularity Hub](https://singularity-hub.org/)
