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
- "Containers can be copied and shared allowing you to replicate your results on a new machine, or allowing colleagues to replicate your results in a different environment."
- "Individuals and organizations distribute software in containers on [Docker Hub](https://hub.docker.com/) and [Singularity Hub](https://singularity-hub.org/)"
- "You can learn more about containers at [Docker Home](https://docs.docker.com/), [Singularity Home](http://singularity.lbl.gov/), and [Singularity at the NIH HPC](https://hpc.nih.gov/apps/singularity.html)."
---

# What's a software container? (And what's it good for?)
Software containers allow you to package an application along with all of its dependencies in a portable, shareable format. Containers package <b>ALL</b> of an apps dependencies... including an entire operating system!  This ensures reproducibility across different computers and environments.  

Containers allow you to do things like:
* Package an analysis pipeline so that it runs on your laptop, in the cloud, and in a high performance computing (HPC) environment to produce the same result.
* Publish all of the software and data from a project along with the paper so that others can reproduce your results.
* Install and run an application that requires a complicated software stack on a new computer with a few keystrokes.

## Containers vs. Virtual Machines
Containers are a type of virtualization and they are related to virtual machines (VMs). But there are a few important differences between the two. A VM has it's own kernel.  This allows the VM to directly access the hardware which allows for more flexibility. For instance, you can run a Linux VM on Windows or on a Mac.  

In contrast, containers share a kernel with the host system.  This makes containers less flexible (a Linux host can typically only support Linux containers), but it also makes them run *much* faster.  

Because of these differences, VMs and containers are useful in different scenarios. If want to interact with your computer using a different operating system, you should usually install a VM.  But if you just need to run one or two apps in a different environment containers are a better choice. 

## Docker   
The most popular and widely used container software is [Docker](https://docs.docker.com/).  Docker is a very mature program with a large user community.  [Docker Hub](https://hub.docker.com/) gives Docker users a place to build and host their containers.  It's fully integrated into the core Docker program, allowing you to download any of over 100,000 pre-built containers from the command prompt.  This arrangement produces a ecosystem in which containers can be easily orchestrated.

Docker is extremely powerful, but it is also a bit difficult to learn.  At first, some of it's inner workings may seem hidden.  For instance, after downloading a container, it may not be immediately clear where that container resides or how it is represented on the local computer.  And Docker is not well-suited for HPC environments where a large number of users share the same storage and operating system.  Still, with its powerful feature set and ecosystem Docker is often the best choice for a new project.

## Singularity
Singularity is a very new program that is still under active development. It is relative easy to use, and it is well-suited for HPC environments. Docker containers can be converted for use with Singularity and current versions of Singularity can import containers directly from Docker Hub. Containers can also be imported from [Singularity Hub](https://singularity-hub.org/).

The philosophy of Singularity differs somewhat from that of Docker.  Docker basically assumes that you will build (or download) and run your containers on the same system, and that you will be a root (administrative) user on that system.  Singularity assumes that you will build your containers on a system where you have root access, but your containers may run in an environment where you are an unprivileged user. In other words, the singularity philosophy assumes you will have a *build system* (a Linux laptop, VM, or cloud instance) where you have root access, and a *production system* where you run your containers (and may or may not have root privileges).   

We will use Singularity for the demonstration below, because it is a little more transparent and easier to learn than Docker.  

## Getting more information about containers
This demo will give you a tiny taste of software containers. If you want more, the following websites are a good place to start:
* [Docker Home](https://docs.docker.com/)
* [Singularity Home](http://singularity.lbl.gov/)
* [Singularity at the NIH HPC](https://hpc.nih.gov/apps/singularity.html)

# Introduction to Singularity
To begin, let's say that you are using a Linux computer with Ubuntu 16.04.

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

You can see that I also have a directory called `singularity`.  It contains Singularity source code that I downloaded from github.  More on that later.  

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
bar  centos.img  singularity
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
bar  centos.img  singularity
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

You may have expected `bar` to disappear once we exited the container, but you can see that it remained. This is because Singularity *binds* a user's home directory into the container when it is initiated.  Singularity blurs the lines between a container and the host system by binding several directories to containers by default.  These include `/home/$USER`, `$PWD`, `/tmp`, `/proc`, `/sys` and a few others.  This convenient feature allows you to install a program to perform some analysis within a container, while reading, analyzing, and writing data to the host system.  

If the default directories don't suit your needs, you can customize which directories Singularity binds into you container.  For instance, if you wanted to read from and write to a directory called `/data` you could bind that directory to your container using the `--bind` argument.  See the documentation at [Singularity Home](http://singularity.lbl.gov/), or [Singularity at the NIH HPC](https://hpc.nih.gov/apps/singularity.html) for more details on this procedure.

# Creating your own Singularity containers
As noted in the introduction, you must have root (administrative) rights on a Linux system to create build and manage Singularity containers.  Once your container is built, you can move it to an environment where you don't have root access (like an HPC system) and run it there.  

## The basics of building containers

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
bar  centos.img  singularity  ubuntu.img  
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

Beneath the copyright information there are several sections.  The first section, the Header, has several keywords (`Bootstrap`, `OSVersion`, and `MirrorURL`) which give Singularity information about how to create the OS, which version to use, and from where to download it.  

The `%runscript` section tells Singularity what this container should do when it is called without any other input.  In this case it will just echo a short message to standard output.  

The `%post` section is used to customize your container.  It tells Singularity what commands should run in the container after the OS is installed.  In this case Singularity will echo a "Hello" message, use use the stream editor `sed` to edit a configuration file, and then use the `apt` package manager to install a text editor (`vim`).

Let's use the `bootstrap` command to install an OS into our container using this definition file as a set of blueprints.

~~~
$ sudo singularity bootstrap ubuntu.img ubuntu.def 
~~~
{: .bash}

~~~
: Retrieving InRelease 
I: Failed to retrieve InRelease
I: Retrieving Release 
I: Retrieving Release.gpg 
I: Checking Release signature
I: Valid Release signature (key id 790BC7277767219C42C86F933B4FE6ACC0B21F32)
I: Retrieving Packages 
I: Validating Packages
[...snip ...]
~~~
{: .output}

Messages like this will continue for several minutes as Singularity downloads, unpacks, and assembles all of the components for an operating system. When bootstrapping finishes, we can use the `shell` command again to start an interactive shell inside the container. 

~~~
$ sudo singularity shell --writable ubuntu.img 
~~~
{: .bash}

~~~
Singularity: Invoking an interactive shell within container...
~~~
{: .output}

~~~
Singularity.ubuntu.img> # bash
~~~
{: .bash}

~~~
root@ip-172-31-18-4:/root# 
~~~
{: .output}

These commands are different than the `shell` command we issued in the previous section.  First, notice that we used the `sudo` program to start a shell in our Singularity container as the root user.  

Second, note the `--writable` option to the `shell` command.  Normally, Singularity containers are *read only* meaning they can't be altered.  But the `--writable` option means we can alter the container when we enter it.  

Finally, notice the `bash` command that we executed after initiating a shell within the container.  The Boure again shell (`bash`) is more convenient to work with than the Bourne shell (`sh`).

Let's make a few changes to our container.

~~~
root@ip-172-31-18-4:/root# apt-get update
~~~
{: .bash}

~~~
Ign http://us.archive.ubuntu.com trusty InRelease
Hit http://us.archive.ubuntu.com trusty Release.gpg
Hit http://us.archive.ubuntu.com trusty Release
Hit http://us.archive.ubuntu.com trusty/main amd64 Packages
Get:1 http://us.archive.ubuntu.com trusty/universe amd64 Packages [5859 kB]
Get:2 http://us.archive.ubuntu.com trusty/main Translation-en [762 kB]
Get:3 http://us.archive.ubuntu.com trusty/universe Translation-en [4089 kB]
Fetched 10.7 MB in 6s (1559 kB/s)
Reading package lists... Done
~~~
{: .output}

~~~
root@ip-172-31-18-4:/root# locale-gen en_US.UTF-8
~~~
{: .bash}

~~~
Generating locales...
  en_US.UTF-8... done
Generation complete.
~~~
{: .output}

~~~
root@ip-172-31-18-4:/root# apt-get -y install cowsay
~~~
{: .bash}

~~~
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following extra packages will be installed:
  libarchive-extract-perl libgdbm3 liblog-message-simple-perl libmodule-pluggable-perl libpod-latex-perl libterm-ui-perl libtext-soundex-perl netbase perl perl-modules
[...snip...]
~~~
{: .output}

~~~
root@ip-172-31-18-4:/root# /usr/games/cowsay 'Cows are crazy for containers!!'
~~~
{: .bash}

~~~
 _________________________________
< Cows are crazy for containers!! >
 ---------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
~~~
{: .output}

To summarize the commands above: 

First we used the package manager `apt` to install updates to our container's operating system.  

Then we used the `locale-gen` command generate a locale instructing software in the container to use the United States dialect of the English language encoded in the UTF-8 character set.  (This is conceptually similar to selecting the language when you install a new operating system.)  

After that, we used the `apt` package manager to install an "important scientific analysis" progam (`cowsay`).  

Finally, we ran our important scientific program (`cowsay`) with some standard input and it produced some standard output.  

This silly example is useful for illustration.  `cowsay` accepts input and produces output.  We will modify our `cowsay` usage below so that it accepts a file as input and produces another file as output.  So if you have a program that you want to run in a container that accepts input and produces output, this example will show you how.

To prepare for the next section, let's exit the container and return to our host system.

~~~
root@ip-172-31-18-4:/root# exit
Singularity.ubuntu.img> exit
$ 
~~~
{: .bash}

## Making containers easier to run
Using the `shell` command to enter a container every time we want to run it is cumbersome.  It would be much better if we could execute a command within a container from the host system command prompt. That is the purpose of the `exec` command.

~~~
$ singularity exec ubuntu.img /usr/games/cowsay "Hey how did you get out of the container?? Let me out too!"
~~~
{: .bash}

~~~
 ________________________________
/ Hey how did you get out of the \
\ container?? Let me out too!    /
 --------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
~~~
{: .output}

The `exec` command instructs Singularity to enter a specified container, look for a specified command, and execute it with the specified input.  

In the Introduction above, we created a file called `~/bar`.  Let's use that file as input to cowsay. 

~~~
$ singularity exec ubuntu.img /usr/games/cowsay $(cat ~/bar)
~~~
{: .bash}

~~~
 _____
< foo >
 -----
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
~~~
{: .output}

The expression `$(cat ~/bar)` is bash syntax for "substitute the standard output of this command here".  As you can see, this caused the containerized `cowsay` program use the contents of `~/bar` as input.  

In addition to using a file as input, let's create another file as output.

~~~
$ singularity exec ubuntu.img /usr/games/cowsay $(cat ~/bar) > output.0
$ ls
~~~
{: .bash}

~~~
bar  centos.img  output.0  singularity  ubuntu.img 
~~~
{: .output}

~~~
$ cat output.0
~~~
{: .bash}

~~~
 _____
< foo >
 -----
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
~~~
{: .output}

To summarize, we now have a containerized "analysis program" (`cowsay`) that accepts a file as input, works on it, and produces a file as output.  Although this is a silly example the general pattern is very useful.

The syntax to run the cowsay container is still quite messy.  It would be nice if there were a cleaner way to run our program.  This is where a runscript comes in handy.  A runscript is a script saved inside of a Singularity container that is executed when the container is called without any other input.  We actually already have a runscript.  Our definion file created one for us.  

~~~
$ ./ubuntu.img
~~~
{: .bash}

~~~
This is what happens when you run the container...
~~~
{: .output}

Let's edit our runscript to produce something more useful. First we will write a script that will take 2 arguments, an input file and an output file, runs cowsay on the input, and then writes the output.

~~~
$ nano new-runscript
~~~
{: .bash}

In the newly opened nano text editor window, we will write the following:

~~~
#!/bin/bash                       
if [ "$#" -ne 2 ]; then               
    echo "Please supply 2 filenames (input and output)"
    exit 1                                
fi                                    
input=$1                              
output=$2                             
/usr/games/cowsay $(cat ${input}) > ${output}
~~~
{: .bash}

In addition to running cowsay on the input and producing output, this script checks that two arguments were supplied and exits early with an error message if that is not the case.  

Now let's copy this new runscript to the appropriate location inside the container with the `singularity copy` command.

~~~
$ sudo singularity copy ubuntu.img new-runscript /singularity
~~~
{: .bash}

Great.  Now let's run it!

~~~
$ ./ubuntu.img 
~~~
{: .bash}

~~~
Please supply 2 filenames (input and output)
~~~
{: .output}

~~~
$ ./ubuntu.img ~/bar output.1
$ cat output.1
~~~
{: .bash}

~~~
 _____
< foo >
 -----
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
~~~
{: .output}

~~~
$ ./ubuntu.img output.1 meta.cow
$ cat meta.cow
~~~
{: .bash}

~~~
 _________________________________________
/ _____ < foo > ----- \ ^__^ \            \
\ (oo)\_______ (__)\ )\/\ ||----w | || || /
 -----------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
~~~
{: .output}

At this point, it might be useful to change the name of `ubuntu.img` to something more fitting (like `cowsay-io` perhaps).  You could even add this container's location to your path, and then the command would be accessible from anywhere on your system.  

Using tricks like these it's possible to install containerized apps that behave as though they were just regular old apps running directly on the host system. But behind the scenes these apps run in a completely different environment and can be copied from one computer to another with ease!

## Fostering reproducibility 
In the previous section, we created a basic image and then used the `shell --writable` command to enter the container as root.  Then we updated the software and installed a new app.  Finally we exited the container, wrote a runscript and copied it into the container.  What if we needed to recreate exactly the same container?  Clearly this method is not very reproducable.  

All of the steps to build this container could be easily encapselated in a defintion file. Here is an exmple of that that would look like:

~~~
BootStrap: debootstrap
OSVersion: trusty
MirrorURL: http://us.archive.ubuntu.com/ubuntu/

%runscript
#!/bin/bash
    if [ "$#" -ne 2 ]; then
    echo "Please supply 2 filenames (input and output)"
    exit 1
fi
input=$1
output=$2
/usr/games/cowsay $(cat ${input}) > ${output}

%post
    locale-gen en_US.UTF-8
    sed -i 's/$/ universe/' /etc/apt/sources.list
    apt-get -y update
    apt-get -y install vim cowsay
~~~
{: .bash}

As a rule, you should try to build your containers using definition files.  One common workflow is to bootstrap a basic container and then edit the container as we did above during testing and debugging.  As you are deciding what needs to be installed in your container, you can make notes in a definition file.  Once you are happy that your container behaves as you like, delete it and build it using the defintion file.  This ensures that you can reproduce your container again in the future.  


# Using pre-built containers from [Docker Hub](https://hub.docker.com/) and [Singularity Hub](https://singularity-hub.org/)
Singularity can download and run containers directly from [Docker Hub](https://hub.docker.com/) and [Singularity Hub](https://singularity-hub.org/). Try running the following command.

~~~
$ singularity run docker://godlovedc/lolcow
~~~
{: .bash}

~~~
Cache folder set to /home/ubuntu/.singularity/docker
Downloading layer sha256:a3ed95caeb02ffe68cdd9fd84406680ae93d633cb16422d00e8a7c22955b46d4
Extracting /home/ubuntu/.singularity/docker/sha256:a3ed95caeb02ffe68cdd9fd84406680ae93d633cb16422d00e8a7c22955b46d4.tar.gz
Downloading layer sha256:339106cb47ef6d14118d525cd927f3ac8bc1b7249a2a19d9b3ca92e069d9ac9e
Extracting /home/ubuntu/.singularity/docker/sha256:339106cb47ef6d14118d525cd927f3ac8bc1b7249a2a19d9b3ca92e069d9ac9e.tar.gz
Downloading layer sha256:6d9ef359eaaa311860550b478790123c4b22a2eaede8f8f46691b0b4433c08cf
Extracting /home/ubuntu/.singularity/docker/sha256:6d9ef359eaaa311860550b478790123c4b22a2eaede8f8f46691b0b4433c08cf.tar.gz
Downloading layer sha256:9654c40e9079e3d5b271ec71f6d83f8ce80cfa6f09d9737fc6bfd4d2456fed3f
Extracting /home/ubuntu/.singularity/docker/sha256:9654c40e9079e3d5b271ec71f6d83f8ce80cfa6f09d9737fc6bfd4d2456fed3f.tar.gz
Downloading layer sha256:e8db7bf7c39fab6fec91b1b61e3914f21e60233c9823dd57c60bc360191aaf0d
Extracting /home/ubuntu/.singularity/docker/sha256:e8db7bf7c39fab6fec91b1b61e3914f21e60233c9823dd57c60bc360191aaf0d.tar.gz
Downloading layer sha256:f8b845f45a87dc7c095b15f3d9661e640ebc86f42cd8e8ab36674846472027f7
Extracting /home/ubuntu/.singularity/docker/sha256:f8b845f45a87dc7c095b15f3d9661e640ebc86f42cd8e8ab36674846472027f7.tar.gz
Downloading layer sha256:d54efb8db41d4ac23d29469940ec92da94c9a6c2d9e26ec060bebad1d1b0e48d
Extracting /home/ubuntu/.singularity/docker/sha256:d54efb8db41d4ac23d29469940ec92da94c9a6c2d9e26ec060bebad1d1b0e48d.tar.gz
 _________________________________________
/ The abuse of greatness is when it       \
| disjoins remorse from power.            |
|                                         |
\ -- William Shakespeare, "Julius Caesar" /
 -----------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
~~~
{: .output}

If you run this command, your cow will probably say something different and will look different too. This container was built using Docker and uploaded to [Docker Hub](https://hub.docker.com/).  If you wanted to download and save this container for later use, you could do so with a definition file.  (We'll call it `lolcow.def`)

~~~
# call this file lolcow.def
Bootstrap: docker
From: godlovedc/lolcow
~~~
{: .bash}

Then create and bootstrap the container as in the example above.

~~~
$ sudo singularity create lolcow.img
$ sudo singularity bootstrap lolcow.img lolcow.def
~~~
{: .bash}

Now you can generate as many quotes as you want by executing `./lolcat.img`!

Once again, this is a trivial example.  But there are over 100,000 pre-built containers already on Docker Hub.  And in addition to individual developers, companies (like Canonical, Anaconda, and NVIDIA to name a few) are also distributing software in ready-to-run containers on Docker Hub. 

For instance, if you wanted to try TensorFlow (the Deep Learning framework used by Google) but you don't want to install a bunch of dependancies on your computer, you could be up and running in a few minutes with this simple definition file.

~~~
BootStrap: docker
From: tensorflow/tensorflow:latest

%runscript
    python "$@"
~~~
{: .bash}

[Singularity Hub](https://singularity-hub.org/) is the Singularity analog to Docker Hub. Singularity Hub is very new and does not yet have the massive community that has been attracted to Docker Hub.  But it has the distict advantage of working natively with Singularity definition files. Like Docker Hub, it integrates with GitHub to build your containers automatically when you push a new definition file to a linked repository.  (See the website for more details.)  This provides a great solution for building and sharing your own containers with others. 


