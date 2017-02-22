---
start: true
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
- "Understand how the components in your computing stack relate to one another"
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


---

## Getting started

* Connect to felix or helix using NoMachine
We'll be conducting this course using a remote desktop utility called [NoMachine](http://www.nomachine.com). You should have already met with the DSST staff to configure and test it. Open the NoMachine App and connect to felix.nimh.nih.gov if you are an NIMH employee or helix.nih.gov if you work for another IC.
* Open Terminal from the Application-> System Tools menu
* Start up an IPython window
We've setup a short [script]() to get you started quickly in the NIH HPC (felix or helix). To run it, type:

~~~
source /data/DSST/scripts/repro_env_setup.sh
~~~
{: .bash}

Your screen should now look something like this:

![image_of_shell](../fig/HPC_desktop.png)

## Know who (or what) you're talking to

It's easy and common to click on an icon, open and window and typing, clicking, and analyzing in that window without much thought about how or where those commands are being executed and where the data is being stored. It's worth the effort to take some time and understand exactly wheat your computing (stack)[] looks like and exactly where everything is happening. Understanding this stack can help you make your analysis more efficient and secure.

## Where am I?

The desktop you're looking at inside the NoMachine window is from a computer that lives over in building 13 at NIH's high performance computing (HPC) center. This computer (helix or felix) is separate from but closely affiliated with the large cluster of computers known as the Biowulf.

NoMachine is a remote desktop program. It allows your to interact with the remote computer (helix/felix) almost as if you were sitting right in front of it. (VNC is another common remote desktop program).

The window on the left of your NX desktop is running an IPython shell. On the right side, there is a window running a (Bash) shell. A (shell)[reference] refers to a program that wraps around another program that is usually more complicated and less user-friendly. That program inside the shell is often referred to as a kernel.

![image_of_shell](../fig/layers_of_computing.png)

For any computer you might be working with, there is a main kernel that is part of the "operating system" at the heart of it.  On top of that kernel there are many other programs running, some of them are designed to provide you with an easy way to interact

# Boxed Text
Bash vs. IPython
We'll be working almost exclusively in the IPython shell in this course. IPython provides an easy way to explore and interact with your data that leverages the power of the Python programming language. The Bash shell is an extremely versatile tool designed to allow you to control and interact with files and your computer more generally. You've likely had exposure to Bash (or it's close cousin, tcsh) if you've used analysis packages like AFNI, FSL, and FreeSurfer. The Bash shell is a (great thing to learn)[Link to bash tutorials], but we want to focus on teaching you reproducible computing concepts without getting bogged down in the syntax of too many different languages.

# Exercise

Draw a diagram to illustrate how the programs and computers listed below relate to one another.

* Your laptop
* Helix & Felix
* The Biowulf cluster
* NoMachine Remote Desktop
* IPython Shell
* Angry Birds on your phone

No get with your partner and compare your drawings. Discuss the difference and edit as needed.



##  The file system
Talk about what a path is etc. using the following figures:
![image_of_shell](../fig/file_system_1.png)
![image_of_shell](../fig/file_system_2.png)
![image_of_shell](../fig/file_system_3.png)

# Exercise

Use the cd command to change to each of these directories in this order:

In each directory, run the following command to create a simple csv text file

echo $PWD,$USER, Was Here, $TIME > $USER_footprint.csv

When you're finished, list your footprint files:
find . -name $USER -exec cat {} \;

Copy the output into the Etherpad


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
