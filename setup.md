---
layout: page
title: "Setup"
permalink: /setup/
---

## NIH HPC setup
For this course we will use [Felix](https://hpc.nih.gov/docs/nimh.html), an NIMH-dedicated high performance
computing resource or, for non-NIMH participants at the NIH, [Helix](https://hpc.nih.gov/systems/). If you don't have an NIH HPC account, please [request one](https://hpc.nih.gov/docs/accounts.html). We will access these computers using the [NoMachine](https://www.nomachine.com/) remote desktop client. To install NoMachine:

* **Windows**
  * Download the [installer](https://www.nomachine.com) and install.
* **Mac OSX**
  * Download the [installer](https://www.nomachine.com) and install.
* **Linux (Ubuntu example)**
  * [Download](https://www.nomachine.com/download/download&id=3) the installer
  to your downloads directory.
  * In the terminal run:

~~~
cd ~/Downloads
sudo dpkg -i nomachine_5.2.11_1_amd64.deb # the name of the downloaded version
~~~
{: bash}

After NoMachine is installed, create a new connection to felix.nimh.nih.gov (for NIMH users) or helix.nih.gov (for non-NIMH users). Maintain the default configuration selections (NX port 4000, no proxy, password authentication).

After using NoMachine to start a remote desktop session on felix (or helix):

Open the terminal application and type:

~~~
source /data/DSST/scripts/repro_env_setup.sh
~~~
{: bash}

You're ready to go after you open the jupyter qtconsole by typing:

~~~
jupyter qtconsole &
~~~
{: bash}

You are now setup for the HPC portion of the class. Some exercises will be
conducted directly on your laptop. Read on below the boxed text on how to
install the needed software.


> ## Under the hood (for those who are interested)
>
> The above script executes the commands listed below. These commands load
> modules on felix to provide access to additional software. Specifically
> conda, git, and the text editor atom. Conda is associated with environments
> (packages of software isolated from each other). In this case we are using
> the environment "py3.5" pre-installed on the NIH HPC resources. The `source
> activate` command selects this conda environment. Since we
> wish to use jupyter qtconsole as our interface to IPython we generate a
> configuration file and then use the unix "sed" text processing utility to add
> atom, as the associated text editor for our work.
> 
> 
> 
>
>> ## See script commands
>> 
>>~~~
>> module load Anaconda
>> module load git
>> source activate py3.5
>> module load atom
>> jupyter qtconsole --generate-config
>> sed -i "/#c.JupyterWidget.editor = ''/a c.JupyterWidget.editor = 'atom'" ~/.jupyter/jupyter_qtconsole_config.py
>>~~~
>> {: .bash}
>{: .solution}
>
{: .challenge}



## A guide to local installation 
Please install the text editor [atom](https://atom.io).

 > ## Click here for Windows
 >  *  Download and install [miniconda](https://conda.io/miniconda.html) if you
 >     do not already have conda installed on your system
 >  
 >  *  Once installed open the Anaconda prompt and type:
 >  
 >~~~
 >   conda create -n create py3.5 python=3.5 jupyter pandas seaborn git
 >~~~
 >{: .source}

 >   * To configure jupyter qtconsole to use atom type the following at the
 >   Anaconda prompt:
 > 
 >~~~
 > jupyter qtconsole --generate-config
 >~~~
 >{: .source}
 > 
 > Then open atom and navigate to the config file listed at the Anaconda prompt.
 > 
 > Edit the line containing the text:
 > 
 >~~~
 > #c.JupyterWidget.editor = ''
 >~~~
 >{: .source}
 > 
 > Change this line to
 > 
 >~~~
 >  c.JupyterWidget.editor = 'atom'
 >~~~
 >{: .source}
 >   * Close atom and the Anaconda prompt. Your system is now set up.
 > 
 {: .solution}
 > ## Click here for Mac OS X
 > 
 > > ## A note to administrators
 > > 
 > >  
 > > * Upon installation Anacaconda prepends itself to the PATH (command placed
 > >   in ~/.bash_profile). This won't work cleanly on many NIH laptops as
 > >   their login shell is set to /bin/sh. Note "echo $SHELL" will still say
 > >   /bin/bash. The login shell should be set to /bin/bash for everything to
 > >   work.
 > >   
 > > * If conda already exists on the laptop (eg. in bash check for output from
 > >   `ls ~|grep conda`) then this can be used to construct a working
 > >   environment for the class:
 > > 
 > > ~~~
 > > conda create -n py3.5 python=3.5 jupyter git pandas seaborn
 > > ~~~
 > > {: .bash}
 > > 
 > > And then modify the qtconsole config file as described below.
 > >   
 > > * Many users wish to have tcsh as they're default shell. Our current
 > >   solution for this is the following: In order to maintain tcsh as their
 > >   login shell and separate the setup for this course as cleanly as
 > >   possible for the user we have installed the terminal application iterm2.
 > >   In the preferences for this application, under the profile tab, is a
 > >   section called "Command". Changing the selection from "Login shell" to
 > >   "Command" and typing /bin/bash here will set all iterm sessions to
 > >   interactive bash sessions. All modifications to the path for these
 > >   sessions must be made in ~/.bashrc instead of ~/.bash_profile. The change
 > >   comprises the package manager conda (an path with anaconda3
 > >   in it in this case) and `/usr/local/bin` if it is not already on the path
 > >   so that the text editor atom works from the command line.
 > >   
 > >  * Installation of atom has posed some problems for people. One easily
 > >    solvable problem is that `/usr/local/bin` is not on the path. The other
 > >    problem has been that for computers where the user does not have
 > >    administrative privileges. The solution to this is the following:
 > > 
 > >  * Download Atom, extract it, move it to applications, select "Authenticate", type in the admin password.
 > >    In bash: 
 > > 
 > > ~~~~
 > > su - admin_user # change as appropriate
 > > sudo /Applications/Atom.app/Contents/Resources/app/atom.sh
 > > ~~~
 > > {: .bash}
 > > 
 > >   After this, in a new iTerm window the editor should be opened by
 > >    executing the command "atom".
 > {: .solution} 
 >    
 >  *  Download and install [miniconda](https://conda.io/miniconda.html) if you
 >     do not already have conda installed on your system
 >  
 >  *  Once installed (The command `which conda` at a terminal should return a path to the installation)
 >~~~
 >   conda create -n create py3.5 python=3.5 jupyter pandas seaborn git
 >~~~
 >{: .source}
 >   
 >   *  To configure jupyter qtconsole to use atom type the following at the
 > terminal prompt:
 >   
 >~~~
 > jupyter qtconsole --generate-config
 > ~~~
 >{: .source}
 > 
 > Then open atom and navigate to the config file listed (probably
 > "~/.jupyter/jupyter_qtconsole_config.py")
 > 
 > Edit the line containing the text:
 > 
 >~~~
 > #c.JupyterWidget.editor = ''
 >~~~
 >{: .source}
 > 
 > Change this line to
 > 
 >~~~
 >  c.JupyterWidget.editor = 'atom'
 >~~~
 >{: .source}
 {: .solution}
 >## Click here for Linux
 >
 >  *  Download and install [miniconda](https://conda.io/miniconda.html) if you
 >     do not already have conda installed on your system
 >  
 >  *  Once installed (The command `which conda` at a terminal should return a path to the installation)
 >~~~
 >   conda create -n create py3.5 python=3.5 jupyter pandas seaborn git
 >~~~
 >{: .source}
 >   
 >   *  To configure jupyter qtconsole to use atom type the following at the
 > terminal prompt:
 >   
 >~~~
 > jupyter qtconsole --generate-config
 > sed -i "/#c.JupyterWidget.editor = ''/a c.JupyterWidget.editor = 'atom'" ~/.jupyter/jupyter_qtconsole_config.py
 >~~~
 >{: .source}
 {: .solution}

 Once the software is installed open a terminal (Linux or Mac OSX) or Anaconda
 prompt (Windows). Now type (same for all operating systems):

~~~
  jupyter qtconsole &
~~~
 {: .source}



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
