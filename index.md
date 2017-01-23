---
layout: lesson
root: .
---
## Re-working of the original material:  

Day 1
+ Layers of computing (10mins)
<!-- all python stuff until data is 120mins -->
+ An introduction to python and ipython (10mins)
    * A key aspect of reproducibility is to use code. Python is a great option for this. (5mins)
    * Introduction to ipython : `pwd`, `cd`, `ls` and system commands (5mins)
+ The basics of python (110mins)    
    * First hour of gapminder course. variables,types,builtin functions. (65mins)
    * Lists, list comprehensions and other loops (45mins)
+ Introduction to the data (20 mins)
    * Brainbox is a great aggregator of data. Explore this.
    * How would we use other peoples tools to achieve our aims.
+ Beginning to work with the data files
    * Segue to libraries with pathlib (20mins)
    * Exploring the features of pathlib (~ 50mins)
        * basic path object with associated commands `exists`, `isdir`, `is_file`, `absolute`, `parent` (object not callable)
        * `joinpath`, `mkdir` (with idempotence), `rmdir`, `chmod`
        * `cd`
        * `relative_to`, `parts`, `parents` (need to turn generator to list)
        * clone data
        * `iterdir`, `glob`, `rglob`
        * `write_text` and `read_text`
        * mention high level methods expecting strings instead of path objects and the `as_uri` or `as_posix` commands
+ wrap up (10mins)
    * adding a series of commands to a file.
    * briefly discuss how we should start to begin to track this.



## original text

This lesson is an introduction to programming in Python
for people with little or no previous programming experience.
It uses plotting as its motivating example,
and is designed to be used in both [Data Carpentry]({{ site.dc_site }})
and [Software Carpentry]({{ site.swc_site }}) workshops.
This lesson references the Jupyter Notebook,
but can be taught using a regular Python interpreter as well.
Please note that this lesson uses Python 3 rather than Python 2.

> ## Under Design
>
> **This lesson is currently in its early design stage;
> please check [the design notes]({{ page.root }}/design/)
> to see what we have so far.
> Contributions are very welcome:
> we would be particularly grateful for exercises
> and for commentary on the ones already there.**
{: .callout}

> ## Prerequisites
>
> 1.  Learners need to understand what files and directories are,
>     what a working directory is,
>     and how to start a Python interpreter.
>
> 2. Learners must install Python before the class starts.
>
> 3. Learners must get the gapminder data before class starts:
>    please download and unzip the file 
>    [python-novice-gapminder-data.zip]({{page.root}}/files/python-novice-gapminder-data.zip).
>
>    Please see [the setup instructions]({{ page.root }}/setup/)
>    for details.
{: .prereq}
