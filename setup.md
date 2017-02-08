---
layout: page
title: "Setup"
permalink: /setup/
---

## Install NoMachine
For this course we will utilize Felix, an NIMH-dedicated high performance
computing resource. In order to use this NoMachine must be installed on your
laptop.

## Windows

## Mac OSX

## Linux
- [Download](https://www.nomachine.com/download/download&id=3) the installer to
your downloads directory.
- In the terminal run:

~~~
cd ~/Downloads
sudo dpkg -i nomachine_5.2.11_1_amd64.deb # the name of the downloaded version
~~~
{: .source}

## Setting up the environment

Open the terminal application and type:
~~~
source /data/DSST/repro_env_setup.sh
~~~
{: .source}

## Open the Jupyter qtconsole

You're ready to go after you type:

~~~
jupyter qtconsole &
~~~
{: .source}




> ## Under the hood (for those who are interested)
>
> The above script executes the commands listed below. These commands load
> modules on felix to provide access to additional software. Specifically the text
> editor atom, the conda package manage with all of its associated environments 
> (packages of softare isolated from each other), and finally the version control
> softare git. The `source activate` command selects the conda environment that we
> wish to use. Since we wish to use jupyter qtconsole as our interface to IPython
> we generate a configuration file and then use the unix "sed" text processing
> utility to add atom, as the associated text editor for our work.
> 
> 
> 
>
>> ## See script commands
>>  ~~~
>> module load atom
>> module load Anaconda
>> module load git
>> source activate py3.5
>> jupyter qtconsole --generate-config
>> sed -i "/#c.JupyterWidget.editor = ''/a c.JupyterWidget.editor = 'atom'" ~/.jupyter/jupyter_qtconsole_config.py
>> ~~~
>> {: .bash}
>{: .solution}
>
{: .challenge}


## Not part of the reproducibility course
##  The rest of this page is to guide local installation if desired in future


## Installing Python Using Anaconda
[Python][python] is a popular language for scientific computing, and great for
general-purpose programming as well. Installing all of its scientific packages
individually can be a bit difficult, however, so we recommend the all-in-one
installer [Anaconda][anaconda].

Regardless of how you choose to install it, please make sure you install Python
version 3.x (e.g., 3.5 is fine). Also, please set up your python environment at 
least a day in advance of the workshop.  If you encounter problems with the 
installation procedure, ask your workshop organizers via e-mail for assistance so
you are ready to go as soon as the workshop begins.

### Windows - [Video tutorial][video-windows]

1. Open [http://continuum.io/downloads][continuum-windows]
   with your web browser.

2. Download the Python 3 installer for Windows.

3. Double-click the executable and install Python 3 using _MOST_ of the
   default settings. The only exception is to check the 
   **Make Anaconda the default Python** option.

4. Install the text editor atom.

5. To setup up a python 3.5 conda environment for the class type (the 2nd and
3rd command are not required if the Anaconda version you downloaded contains a
 python 3.5 environment as the default environment):
~~~
conda config --add channels conda-forge
conda create -n py3.5 python=3.5 anaconda # this will take a long time
activate py3.5 # you will always need to type this to use the environment
conda install -y git 
conda update -y ipython
~~~
{: .source}

6. Configure jupyter qtconsole to use atom:
Type the following at the Anaconda prompt

~~~
jupyter qtconsole --generate-config
~~~
{: .source}

Then open atom and navigate to the config file listed at the Anaconda prompt.

Edit the line containing the text:
~~~
#c.JupyterWidget.editor = ''
~~~
{: .source}
~~~
 c.JupyterWidget.editor = 'atom'
~~~
{: .source}

7. Close atom and the Anaconda prompt. Your system is now set up. From now on to
work with this software open the Anaconda prompt:

~~~
activate py 3.5 # if this is what you named your environment
jupyter qtconsole &
~~~
{: .source}




### Mac OS X - [Video tutorial][video-mac]

1. Open [http://continuum.io/downloads][continuum-mac]
   with your web browser.

2. Download the Python 3 installer for OS X.

3. Install Python 3 using all of the defaults for installation.

### Linux

Note that the following installation steps require you to work from the shell. 
If you run into any difficulties, please request help before the workshop begins.

1.  Open [http://continuum.io/downloads][continuum-linux] with your web browser.

2.  Download the Python 3 installer for Linux.

3.  Install Python 3 using all of the defaults for installation.

    a.  Open a terminal window.

    b.  Navigate to the folder where you downloaded the installer

    c.  Type

    ~~~
    $ bash Anaconda3-
    ~~~
    {: .bash}

    and press tab.  The name of the file you just downloaded should appear.

    d.  Press enter.

    e.  Follow the text-only prompts.  When the license agreement appears (a colon
        will be present at the bottom of the screen) hold the down arrow until the 
        bottom of the text. Type `yes` and press enter to approve the license. Press 
        enter again to approve the default location for the files. Type `yes` and 
        press enter to prepend Anaconda to your `PATH` (this makes the Anaconda 
        distribution the default Python).


## Starting Python

We will teach Python using the [Jupyter qtconsole][jupyter]. This provides an
 command line interface to an IPython kernel. If you installed Python using
 Anaconda, Jupyter should already be on your system. Using the package manager
 conda is the best way to install jupyter. If you don't want to install Anaconda
 you could install miniconda and then use the conda package manager to install
 Jupyter.

To start the console, open a terminal or git bash and type the command:

~~~
$ jupyter qtconsole
~~~
{: .bash}

To start the Python interpreter without the notebook, open a terminal 
or Git Bash and type the command:

~~~
$ python
~~~
{: .bash}

[anaconda]: https://www.continuum.io/anaconda
[continuum-mac]: http://continuum.io/downloads#_macosx
[continuum-linux]: http://continuum.io/downloads#_unix
[continuum-windows]: http://continuum.io/downloads#_windows
[gapminder]: http://gapminder.org
[jupyter]: http://jupyter.org/
[jupyter-install]: http://jupyter.readthedocs.io/en/latest/install.html#optional-for-experienced-python-developers-installing-jupyter-with-pip
[python]: https://python.org
[video-mac]: https://www.youtube.com/watch?v=TcSAln46u9U
[video-windows]: https://www.youtube.com/watch?v=xxQ0mzZ8UvA
