---
title: "The layers of computing"
teaching: 20
exercises: 0
questions:
- "Where, exactly, is my data? Where should it be?"
- "Where is the computer analyzing my data? Can I make it go faster?"
- "How do all of these places relate to each other?"
- "What is the shell and why do I care?"
- "What is python? What is IPython? What is Juypter?"
- "What are the tools we'll be using in the course?"
objectives:
- "Build a mental model of data storage, computing, and how they relate to one another"
- "Understand the different ways of interacting with your computer and what the pros and cons are"
- "Explain when and why command-line interfaces should be used instead of graphical interfaces."
- "Explain the advantages of remote computing including cloud and high performance computing."
- "Explain how to access the NIMH dedicated computing resources in the most convenient manner."
- "Get exposed to IPython and learn it's strengths."
- "Learn shortcuts and hotkeys to make command line computing fast and efficient"
keypoints:
- "A shell is a program whose primary purpose is to read commands and run other
programs."
- "The shell’s main advantages are its high action-to-keystroke ratio, its
support for automating repetitive tasks, and that it can be used to access
networked machines."
- "The shell’s main disadvantages are its primarily textual nature and how
cryptic its commands and operation can be."
- "We will work on a remote instance of the linux operating system"
- "Although there are many ways to work remotely, we will use a graphical
interface using NoMachine"
- "We will use an IPython console to interact with the Python interpretter"
- "We can easily interact with the system shell from IPython"

---

## Getting started

### Open NoMachine

### Get an IPython window starter



## Layers of computing


Talk about the layers of computing and where the shell and other higher level
programs fit into this. Mention remote computing.

![image_of_shell](../fig/layers_of_computing.png)


##  The file system
Talk about what a path is etc. using the following figures:
![image_of_shell](../fig/file_system_1.png)
![image_of_shell](../fig/file_system_2.png)
![image_of_shell](../fig/file_system_3.png)


## The IPython console
Show 

*  Getting the current working directory with `pwd`
*  navigating the file system with `cd`
*  Listing directories with `ls`
*  How these commands are both Ipthon and system commands.
*  Show how `cd`  behaves differently because each system call is a subprocess
*  Mention how none of this is not python, which is the majority of what we will
teach from now on.

~~~
pwd
~~~
{: .source}
~~~
ls
~~~
{: .source}
~~~
cd Documents
~~~
{: .source}
~~~
ls
~~~
{: .source}
~~~
!pwd
~~~
{: .source}
~~~
!ls
~~~
{: .source}
~~~
!cd Documents
~~~
{: .source}
~~~
ls
~~~
{: .source}
~~~
!mkdir ~/reproducibility_course
~~~
{: .source}
~~~
cd reproducibility_course
~~~
{: .source}



## Convenient commands to remember

*   Use tab completion when possible. The computer is more precise than we are.
*   We can cycle through previous commands using up and down arrows.
*   We can cycle through previous commands starting with the current text using
Ctl + n/p
*   Enter,  Ctl + Enter / Shift + Enter allow us to run commands in different
ways
