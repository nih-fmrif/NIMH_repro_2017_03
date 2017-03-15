---
title: Debugging
teaching: 10
exercises: 0
questions:
- "How can I debug my program?"
objectives:
- "Debug code containing an error systematically."
- "Identify ways of making code less error-prone and more easily tested."
- "Know of the ways to debug using Python and IPython debugging tools in Pycharm, qtconsole, and the ipython console"
keypoints:
---
## Pdb and ipdb
*   The python [debugger](https://docs.python.org/3/library/pdb.html) is a
    command line debugger that can be invoked from a system terminal using the
    command `python -m pdb myscript.py`.
* ipdb provides additional functionality.


> ## Debugging in jupyter qtconsole
> 
> When we have an error in a script while using the run magic in qtconsole we
> do not see any output. This is an known error in qtconsole. Two options exist
> at this point.
> 
> We can run the script in debugger mode using the -d flag. This will allow us
> to exam the variables as we execute the script. We will see the exception
> raised by our assert statement in this case. The other option is to use the
> ipython console. This provides a similar interface to ipython but does not
> support inline graphics.
> 
> 
> In addition to this bug the qtconsole does not have readline support for the
> debugger. This means that we must type commands ourselves without relying on
> the arrow keys to  recover previous input.
> 
{: .callout}

## ipdb reference


[This](http://bashdb.sourceforge.net/pydb/pydb/lib/subsubsection-brkpts.html) is helpful.
And scipy [lectures](http://www.scipy-lectures.org/advanced/debugging/)


    # In order to debug a function in qtconsole:
    from IPython.core.debugger import Pdb; ipdb=Pdb()
    ipdb.runcall(foo, 1, 2)
Found [here](http://stackoverflow.com/questions/12646670/stepping-into-a-function-in-ipython):

After a runtime error use the debug magic to inspect the variables when execution failed:

~~~
%debug
~~~
{: .python}

Finally, run a file in debug mode using the `-d` flag to the run magic:

~~~
%run -d metasearch_analysis.py
~~~
{: .python}


----Getting help ----

    # display commands:
    ? 
    # display help for w:
    ?w 

----Getting Context----

    # where in the current call stack:
    w 
    # long list of code surrounding current location of execution:
    ll  
    # list shorter context:
    l
    # list local variables:
    dir()
    # list arguments to current function:
    a
    # print variable X
    p X
    # pretty print variable X
    pp X

---- Controlling execution ----    

    # continue until the next breakpoint:
    c 
    # execute the next line:
    n 
    # execute the current line. stop at the first occasion
    # 
    # temporary  breakpoint here:
    tbreak 5 
    # no arguments lists them:
    break 
    # breakpoint at line 5:
    b 5 
    # clear breakpoint number 2:
    cl 2 
    # ignore breakpoint 1 for the next 3 crossings:
    ignore 1 3 
