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

We will use Singularity for the demonstration below.  

## Getting more information about containers
This demo will only give you a brief taste of software containers. If you want to learn more, the following websites will give you a good place to start:
* [Docker Home](https://docs.docker.com/)
* [Singularity Home](http://singularity.lbl.gov/)
* [Singularity at the NIH HPC](https://hpc.nih.gov/apps/singularity.html)

# Introduction to Singularity

~~~
singularity shell some.img
~~~
{: .bash}

~~~
~~~
{: .output}



* Starts a new shell in the container `some.img`

# Creating your own Singularity containers
* Basics
* Advanced techniques

# Using pre-built containers from [Docker Hub](https://hub.docker.com/) and [Singularity Hub](https://singularity-hub.org/)
