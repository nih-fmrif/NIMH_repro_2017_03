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
* containers allow you to do lots of things
* they differ from VMs

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
