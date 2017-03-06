---
title: "Libraries and pathlib"
teaching: 15
exercises: 15
questions:
- "How can I use software that other people have written?"
- "How can I find out what that software does?"
objectives:
- "Explain what software libraries are and why programmers create and use them."
- "Write programs that import and use libraries from Python's standard library."
- "Find and read documentation for standard libraries interactively (in the interpreter) and online."
keypoints:
- "Most of the power of a programming language is in its libraries."
- "A program must import a library in order to use it."
- "Use `help` to find out more about a library's contents."
- "Import specific items from a library to shorten programs."
- "Create an alias for a library when importing it to shorten programs."
---

## Most of the power of a programming language is in its libraries.

*   A *library* is a collection of functions that can be used by other programs.
    *   May also contain data values (e.g., numerical constants).
    *   Library's contents are supposed to be related, but there's no way to enforce that.
*   Python's [standard library][stdlib] is installed with it.
*   Many additional libraries are available from [PyPI][pypi] (the Python Package Index).
*   We will see later how to write new libraries.

## A program must import a library in order to use it.

*   Use `import` to load a library into a program's memory.
*   Then refer to things from the library as `library_name.thing_name`.
    *   Python uses `.` to mean "part of".

~~~
import math

print('pi is', math.pi)
print('cos(pi) is', math.cos(math.pi))
~~~
{: .python}
~~~
pi is 3.141592653589793
cos(pi) is -1.0
~~~
{: .output}

*   Have to refer to each item with the library's name.
    *   `math.cos(pi)` won't work: the reference to `pi`
        doesn't somehow "inherit" the function's reference to `math`.

## Use `help` to find out more about a library's contents.

*   Works just like help for a function.

~~~
help(math)
~~~
{: .python}
~~~
Help on module math:

NAME
    math

MODULE REFERENCE
    http://docs.python.org/3.5/library/math

    The following documentation is automatically generated from the Python
    source files.  It may be incomplete, incorrect or include features that
    are considered implementation detail and may vary between Python
    implementations.  When in doubt, consult the module reference at the
    location listed above.

DESCRIPTION
    This module is always available.  It provides access to the
    mathematical functions defined by the C standard.

FUNCTIONS
    acos(...)
        acos(x)

        Return the arc cosine (measured in radians) of x.
⋮ ⋮ ⋮
~~~
{: .output}

## Import specific items from a library to shorten programs.

*   Use `from...import...` to load only specific items from a library.
*   Then refer to them directly without library name as prefix.

~~~
from math import cos, pi

print('cos(pi) is', cos(pi))
~~~
{: .python}
~~~
cos(pi) is -1.0
~~~
{: .output}

## Create an alias for a library when importing it to shorten programs.

*   Use `import...as...` to give a library a short *alias* while importing it.
*   Then refer to items in the library using that shortened name.

~~~
import math as m

print('cos(pi) is', m.cos(m.pi))
~~~
{: .python}
~~~
cos(pi) is -1.0
~~~
{: .output}

*   Commonly used for libraries that are frequently used or have long names.
    *   E.g., Numpy numeric analysis library is often aliased to np. The pandas
        library for dataframes is often aliased to pd.
*   But can make programs harder to understand, since readers must learn your
    program's aliases.


## Working with the pathlib library
Since we have downloaded a lot of files as part of the metasearch repository we
would like to use a library that will allow us to work with these files more
efficiently. The pathlib library is ideal for this. Let's import from this to
start working with paths:

~~~
from pathlib import Path
~~~
{: .python}

*   We use the Path class in the pathlib library to create Path objects, which
    we can then use for subsequent processing. To create a new path object we
    provide a name as the first argument. This name is a string representation of a
    path. We will create a Path object that represents the directory we downloaded:

~~~
metasearch_dir = Path('metasearch')
print(metasearch_dir)
~~~
{: .python}
~~~
metasearch
~~~
{: .output}

*   The `absolute()` method can be used to convert a relative path to an
    absolute path:

~~~
print(metasearch_dir.absolute())
~~~
{: .python}
~~~
/home/username/reproducibility_course/metasearch
~~~
{: .output}

## Data descriptors of a Path object

In addition to some convenient methods to work with filesystem paths the
metasearch_dir object has more useful things to help us when we work with
paths.  More specifically it has what are termed data descriptors. These are
accessed in a similar manner to the methods but without parentheses. As an
example we'll use the `parent` data descriptor:


~~~
print(metasearch_dir.parent)        
~~~
{: .python}
~~~
PosixPath('.')
~~~
{: .output}

In this case the descriptor is not particularly useful because metasearch_dir
is specified as a relative path. We can use the `absolute()` method to fix this:

~~~
print(metasearch_dir.absolute().parent)
~~~
{: .python}
~~~
PosixPath('/home/rodgersleejg/reproducibility_course')
~~~
{: .output}

Another example of a useful Path data descriptor is the `name` attribute:

~~~
metasearch_dir.name
~~~
{: .python}
~~~
'metasearch'
~~~
{: .output}

 An error occurs if we attempt to call a data descriptor as if it were a
 method:

 ~~~
 metasearch_dir.name()
 ~~~
 {: .python}
 ~~~
 ---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-328-b6f442f14303> in <module>()
----> 1 metasearch_dir.name()

TypeError: 'str' object is not callable
 ~~~
 {: .output}

 If we try to use a method as if it were a data descriptor nothing useful is
 displayed:

 ~~~
 metasearch_dir.absolute
 ~~~
 {: .python}
 ~~~
  <bound method Path.absolute of PosixPath('metasearch')>
 ~~~
 {: .output}

If we keep track of what is a method and what is a data-descriptor it helps us
to avoid these mistakes. We can view the data-descriptors at the end of the
help for the Path class from the pathlib library:

~~~
help(Path)
~~~
{: .python}
~~~

   ⋮ ⋮ ⋮ 

 |  ----------------------------------------------------------------------
 |  Data descriptors inherited from PurePath:
 |  
 |  anchor
 |      The concatenation of the drive and root, or ''.
 |  
 |  drive
 |      The drive prefix (letter or UNC path), if any.
 |  
 |  name
 |      The final path component, if any.
 |  
 |  parent
 |      The logical parent of the path.
 |  
 |  parents
 |      A sequence of this path's logical parents.
 |  
 |  parts
 |      An object providing sequence-like access to the
 |      components in the filesystem path.
 |  
 |  root
 |      The root of the path, if any.
 |  
 |  stem
 |      The final path component, minus its last suffix.
 |  
 |  suffix
 |      The final component's last suffix, if any.
 |  
 |  suffixes
 |      A list of the final component's suffixes, if any.
~~~
{: .output}



*   The concrete path classes include a `resolve()` method for normalizing a path by looking at the filesystem for directories and producing the absolute path referred to by a name. Symlinks will be resolved and on Windows slashes will be replaced with backslashes. 

~~~
print(metasearch_dir.resolve())
~~~
{: .python}


*   Given an existing path object, it is easy to build a new one with minor differences such as referring to a different file in the same directory. Use `with_name()` to create a new path that replaces the name portion of a path with a different file name. Use `with_suffix()` to create a new path that replaces the file name’s extension with a different value.

~~~
crawler_dir = metasearch_dir.joinpath('crawler')
py = crawler_dir.with_name('transform.py')
print(py)

ipynb = py.with_suffix('.ipynb')
print(ipynb)
~~~
{: .python}
~~~
metasearch/transform.py
metasearch/transform.ipynb
~~~
{: .output}


## Constructing paths with multiple directory arguments

*   We can build up a path by providing directories to the joinpath(). We pass each path segment as a separate argument:

~~~
metadata_dir = metasearch_dir.joinpath('crawler', 'metadata')
print(metadata_dir)
~~~
{: .python}

~~~
metasearch/crawler/metadata
~~~
{: .output}

It's worth noting that if we want to pass multiple arguments into a function
like this can be done by unpacking using the star operator:
~~~
subdirs = ['crawler', 'metadata']
metadata_dir = metasearch_dir.joinpath(*subdirs)
print(metadata_dir)
~~~
{: .python}
~~~
metasearch/crawler/metadata
~~~
{: .output}

While it's convenient to construct these paths we should remember that we don't
necessarily know whether the path that we have created exists. In order to
check this we can use the exists() method:

~~~
print(metadata_dir.exists())
~~~
{: .python}
~~~
True
~~~
{: .output} 


------------------------- Below this is still being developed -------------------------


## Working with multiple Paths

*   The Path object can be iterated, for example using list comprehension, discussed previously, in order to retrieve all the files (and subdirectories) that live within that particular path.
*   If the Path does not refer to a directory, `iterdir()` raises NotADirectoryError.

~~~
[x for x in metasearch_dir.iterdir()]
~~~
{: .python}



*   Use `glob()` to find only files matching a pattern.

~~~
some_dir_with_csv = metasearch_dir.joinpath('crawler', 'clean-csv').resolve()
%cd $some_dir_with_csv
for f in some_dir_with_csv.glob('*.csv'):
    print(f)
    ~~~
{: .python}

*   The glob processor supports recursive scanning using the pattern prefix ** or by calling `rglob()` instead of `glob()`. Multiple wildcards can be passed to glob methods.

~~~
for f in metasearch_dir.rglob('*-*.csv'):
    print(f)
~~~
{: .python}

## Reading and Writing Files

*   Each Path instance includes methods for working with the contents of the file to which it refers. For immediately retrieving the contents, use `read_bytes()` or `read_text()`. Use the `open()` method to open the file and retain the file handle, instead of passing the name to the built-in `open()` function.

~~~
some_csvs = [x for x in metasearch_dir.rglob('*-*.csv')]
some_csv = some_csvs[0]
with some_csv.open('r', encoding='utf-8') as handle:
    print('read from open(): {!r}'.format(handle.read()))

print('read_text(): {!r}'.format(f.read_text('utf-8')))
~~~
{: .python}

*   To write to the file, use `write_bytes()` or `write_text()`.

~~~
f = metasearch_dir.joinpath('example.txt')
f.write_bytes('This is the content'.encode('utf-8'))
~~~
{: .python}

*   This will create the file if it does not exist and overwrite exiting content if it does.

~~~
%cat $metasearch_dir/ex*
~~~
{: .python}

## File Properties

*   Detailed information about a file can be accessed using the methods stat().

~~~
stat_info = f.stat()

import time
print('{}:'.format(f))
print('  Size (kB)    :', stat_info.st_size)
print('  Created      :', time.ctime(stat_info.st_ctime))
print('  Last modified:', time.ctime(stat_info.st_mtime))
print('  Last accessed:', time.ctime(stat_info.st_atime))
~~~
{: .python}

## Deleting

*   For testing if a particular Path object corresponds to an actual file use `exists()`.
*   For removing files use unlink().

~~~
print('exists before removing:', f.exists())
f.unlink()
print('exists after removing:', f.exists())
~~~
{: .python}








> ## Exploring the Math Library
>
> 1. What function from the `math` library can you use to calculate a square root
>    *without* using `sqrt`?
> 2. Since the library contains this function, why does `sqrt` exist?
{: .challenge}

> ## Locating the Right Library
>
> You want to select a random character from a string:
> ~~~
> bases = 'ACTTGCTTGAC'
> ~~~
>
> 1. What [standard library][stdlib] would you most expect to help?
> 2. Which function would you select from that library? Are there alternatives?
{: .challenge}

> ## When Is Help Available?
>
> When a colleague of yours types `help(math)`,
> Python reports an error:
>
> ~~~
> NameError: name 'math' is not defined
> ~~~
> {: .error}
>
> What has your colleague forgotten to do?
{: .challenge}

> ## Importing With Aliases
>
> 1. Fill in the blanks so that the program below prints `90.0`.
> 2. Rewrite the program so that it uses `import` *without* `as`.
> 3. Which form do you find easier to read?
>
> ~~~
> import math as m
> angle = ____.degrees(____.pi / 2)
> print(____)
> ~~~
> {: .python}
{: .challenge}

> ## Importing Specific Items
>
> 1. Fill in the blanks so that the program below prints `90.0`.
> 2. Do you find this easier to read than preceding versions?
> 3. Why *would't* programmers always use this form of `import`?
>
> ~~~
> ____ math import ____, ____
> angle = degrees(pi / 2)
> print(angle)
> ~~~
> {: .python}
{: .challenge}

> ## Identifying Input Variable Range Error
>
> 1. Read the code below and try to identify what the errors are without running it.
> 2. Run the code, and read the error message. What type of error is it?
> 3. Fix the error.
>
> ~~~
> from math import log
> log(0)
> ~~~
> {: .python}
{: .challenge}

[pypi]: https://pypi.python.org/pypi/
[stdlib]: https://docs.python.org/3/library/
