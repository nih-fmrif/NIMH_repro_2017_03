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

## What's a software container? (And what's it good for?)
Software containers allow you to package an application along with all of its dependencies in a portable, shareable format. Containers package <b>ALL</b> of an apps dependencies... including the operating system!  This ensures reproducibility across different computers and environments.  Containers allow you to do things like:

* Package an analysis pipeline so that it runs on your laptop, in the cloud, and in a high performance computing (HPC) environment and produces the same result.
* Publish all of the software and data from a project along with the paper so that others can reproduce your results.
* Install and run an application that requires a complicated software stack on a new computer with a few keystrokes.

Containers are a type of virtualization and they are related to virtual machines (VMs).    
[Singularity Home](http://singularity.lbl.gov/)
[Singularity at the NIH HPC](https://hpc.nih.gov/apps/singularity.html)

## Introduction to Singularity

~~~
singularity shell some.img
~~~
{: .bash}

~~~
~~~
{: .output}



* Starts a new shell in the container `some.img`

## Creating your own Singularity containers
* Basics
* Advanced techniques

## Using pre-built containers from [Docker Hub](https://hub.docker.com/) and [Singularity Hub](https://singularity-hub.org/)
