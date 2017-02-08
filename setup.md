---
layout: page
title: "Setup"
permalink: /setup/
---

## Install NoMachine
For this course we will utilize Felix, an NIMH-dedicated high performance
computing resource. In order to use this NoMachine must be installed on your
laptop.

* Windows
  * Download the [installer](https://www.nomachine.com) and install.
* Mac OSX
  * Download the [installer](https://www.nomachine.com) and install.
* Linux (Ubuntu example)
  * [Download](https://www.nomachine.com/download/download&id=3) the installer
  to your downloads directory.
  * In the terminal run:

~~~
cd ~/Downloads
sudo dpkg -i nomachine_5.2.11_1_amd64.deb # the name of the downloaded version
~~~
{: bash}

## Setting up the environment on the NIH cluster

Once logged in to felix (or helix) using NoMachine open the terminal application
and type:
~~~
source /data/DSST/repro_env_setup.sh
~~~
{: bash}

## Open the Jupyter qtconsole

You're ready to go after you type:

~~~
jupyter qtconsole &
~~~
{: bash}




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



> ##  A guide for local installation if desired in future
>
>We used python 3.5 for the course. Any later version of python will also work
>fine. Most of the packages in our environment are contained in the
>Continuum analytics Anaconda environment. Alternatively you can install
>miniconda and install required modules as you require them.
>
>> ## Windows - [Video tutorial][video-windows]
>>   * Open [http://continuum.io/downloads][continuum-windows]
>>    with your web browser.
>>   * Download the Python 3 installer for Windows.
>>   * Double-click the executable and install Python 3 using _MOST_ of the
>>    default settings. The only exception is to check the 
>>    **Make Anaconda the default Python** option.
>>   * Install the text editor atom.
>>   * Make sure you have ipython 5.2.X rather than 5.1.X in the environment 
>> (debugging does not always work in the latter). Also install git if you don't
>> already have it:
>> 
>>   ~~~
>>   conda config --add channels conda-forge
>>   conda install -y git 
>>   conda update -y ipython
>>   ~~~
>>   {: .source}
>>   * To configure jupyter qtconsole to use atom type the following at the
>>   Anaconda prompt:
>> 
>> ~~~
>> jupyter qtconsole --generate-config
>> ~~~
>> {: .source}
>> 
>> Then open atom and navigate to the config file listed at the Anaconda prompt.
>> 
>> Edit the line containing the text:
>> ~~~
>> #c.JupyterWidget.editor = ''
>> ~~~
>> {: .source}
>> 
>> Change this line to
>> ~~~
>>  c.JupyterWidget.editor = 'atom'
>> ~~~
>> {: .source}
>>   * Close atom and the Anaconda prompt. Your system is now set up.
>> 
>{: .solution}
>
>
>> ## Mac OS X - [Video tutorial][video-mac]
>>   * Open [http://continuum.io/downloads][continuum-mac]
>>    with your web browser.
>>   * Download the Python 3 installer for OS X.
>>   * Install Python 3 using all of the defaults for installation.
>> 
>>   * Make sure you have ipython 5.2.X rather than 5.1.X in the environment 
>> (debugging does not always work in the latter). Also install git if you don't
>> already have it:
>> 
>>   ~~~
>>   conda config --add channels conda-forge
>>   conda update -y ipython
>>   ~~~
>>   {: .source}
>>   
>>   *  To configure jupyter qtconsole to use atom type the following at the
>> terminal prompt:
>>   
>>   ~~~
>> jupyter qtconsole --generate-config
>> sed -i "/#c.JupyterWidget.editor = ''/a c.JupyterWidget.editor = 'atom'" ~/.jupyter/jupyter_qtconsole_config.py
>>   ~~~
>>   {: .source}
>{: .solution}
>
>
>>## Linux
>>
>>  *  Open [http://continuum.io/downloads][continuum-linux] with your web browser.
>>  *  Download the Python 3 installer for Linux.
>>  *  Install Python 3 using all of the defaults for installation.
>>
>>  *     Open a terminal window.
>>
>>  *  Navigate to the folder where you downloaded the installer
>>
>>  *  Type
>>
>>    ~~~
>>    $ bash Anaconda3-
>>    ~~~
>>    {: .bash}
>>
>>    and press tab.  The name of the file you just downloaded should appear.
>>
>>  *  Press enter.
>>
>>  *  Follow the text-only prompts.  When the license agreement appears (a colon
>>        will be present at the bottom of the screen) hold the down arrow until the 
>>        bottom of the text. Type `yes` and press enter to approve the license. Press 
>>        enter again to approve the default location for the files. Type `yes` and 
>>        press enter to prepend Anaconda to your `PATH` (this makes the Anaconda 
>>        distribution the default Python).
>>
>>   * Make sure you have ipython 5.2.X rather than 5.1.X in the environment 
>> (debugging does not always work in the latter). Also install git if you don't
>> already have it:
>> 
>>   ~~~
>>   conda config --add channels conda-forge
>>   conda update -y ipython
>>   ~~~
>>   {: .source}
>>   
>>   *  To configure jupyter qtconsole to use atom type the following at the
>> terminal prompt:
>>   
>>   ~~~
>> jupyter qtconsole --generate-config
>> sed -i "/#c.JupyterWidget.editor = ''/a c.JupyterWidget.editor = 'atom'" ~/.jupyter/jupyter_qtconsole_config.py
>>   ~~~
>>   {: .source}
>{: .solution}
>
> With the software installed open a terminal (Linux or Mac OSX) or Anaconda
> prompt (Windows). If you did not install into the default conda environment
> you must activate it. For windows type:
>   ~~~
> activate environment_name
>   ~~~
>   {: .source}
>
> For Linux and OSX:
>   ~~~
> source activate environment_name
>   ~~~
>   {: .source}
> Then type (same for all operating systems):
>   ~~~
> jupyter qtconsole &
>   ~~~
>   {: .source}
{: .challenge}


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
