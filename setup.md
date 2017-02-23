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

We will use python 3.5 for the course. Any later version of python will also work
fine. Most of the packages in our environment are contained in the
[Continuum analytics Anaconda](https://www.continuum.io/) environment. Alternatively you can install
[miniconda](https://conda.io/miniconda.html) and install modules as you require them.

 > ## Click here for Windows
 >   * Anaconda installation:
 >      *  Open [http://continuum.io/downloads][continuum-windows]
 >    with your web browser.
 >      * Download the Python 3 installer for Windows.
 >      * Double-click the executable and install Python 3 using _MOST_ of the
 >    default settings. The only exception is to check the 
 >    **Make Anaconda the default Python** option.
 >   
 >   There is a [video tutorial][video-windows] for anaconda installation if
 >   necessary. 
 >   
 >   In addition to installing Anaconda follow the other
 >   instructions below
 >   
 >   * Make sure you have ipython 5.2.X rather than 5.1.X in the environment 
 > (debugging does not always work in the latter). Also install git if you don't
 > already have it:
 > 
 >~~~
 >   conda config --add channels conda-forge
 >   conda install -y git 
 >   conda update -y ipython
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
 >   * Anaconda installation:
 >      * Download the Python 3 installer for OS X.
 >      * Open [http://continuum.io/downloads][continuum-mac]
 >    with your web browser.
 >      * Install Python 3 using all of the defaults for installation.
 >   
 >   There is a [video tutorial][video-mac] for anaconda installation if
 >   necessary. 
 >   
 >   In addition to installing Anaconda follow the other
 >   instructions below
 > 
 >   * Make sure you have ipython 5.2.X rather than 5.1.X in the environment 
 > (debugging does not always work in the latter). Also install git if you don't
 > already have it:
 > 
 >~~~
 >   conda config --add channels conda-forge
 >   conda update -y ipython
 >   # if the command "git --version" returns an error or a version less than 2.7:
 >   conda install git 
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
 >  *  Open [http://continuum.io/downloads][continuum-linux] with your web browser.
 >  *  Download the Python 3 installer for Linux.
 >  *  Install Python 3 using all of the defaults for installation.
 >
 >  *     Open a terminal window.
 >
 >  *  Navigate to the folder where you downloaded the installer
 >
 >  *  Type
 >
 >~~~
 >    bash Anaconda3-
 >~~~
 >    {: .bash}
 >
 >    and press tab.  The name of the file you just downloaded should appear.
 >
 >  *  Press enter.
 >
 >  *  Follow the text-only prompts.  When the license agreement appears (a colon
 >        will be present at the bottom of the screen) hold the down arrow until the 
 >        bottom of the text. Type `yes` and press enter to approve the license. Press 
 >        enter again to approve the default location for the files. Type `yes` and 
 >        press enter to prepend Anaconda to your `PATH` (this makes the Anaconda 
 >        distribution the default Python).
 >
 >   * Make sure you have ipython 5.2.X rather than 5.1.X in the environment 
 > (debugging does not always work in the latter). Also install git if you don't
 > already have it:
 > 
 >~~~
 >   conda config --add channels conda-forge
 >   conda update -y ipython
 >   # if the command "git --version" returns an error or a version less than 2.7:
 >   conda install git    
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
