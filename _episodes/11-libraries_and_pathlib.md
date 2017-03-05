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
    *   E.g., `matplotlib` plotting library is often aliased as `mpl`.
*   But can make programs harder to understand,
    since readers must learn your program's aliases.









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

*   After cloning the OpenNeuroLab [metasearch](https://github.com/OpenNeuroLab/metasearch) repository, open the directory, i.e.

~~~
%cd ~/gits/metasearch
~~~

*   A program must import a library in order to use it.

*   Use `import` to load a library into a program's memory.

~~~
import pathlib
~~~

## Building Paths and Directory Contents with pathlib

*   Refer to things from the imported library as `library_name.thing_name`.
    *   Python uses `.` to mean "part of".
*   For example, to instantiate a new path, give a string as the first argument. The string representation of the path object is this name value. This example demonstrates printing this string representation for the metasearch repository that you have cloned from github.

~~~
metasearch_dir = pathlib.Path('.')
print(metasearch_dir)
~~~

*   The concrete path classes include a `resolve()` method for normalizing a path by looking at the filesystem for directories and producing the absolute path referred to by a name.

~~~
print(metasearch_dir.resolve())
~~~

*   The Path object can be iterated, for example using list comprehension, discussed previously, in order to retrieve a all the files (and subdirectories) that live within that particular path.
*   If the Path does not refer to a directory, `iterdir()` raises NotADirectoryError.

~~~
[x for x in metasearch_dir.iterdir()]
~~~

*   Use help to find out more about a library’s contents.

~~~
help(pathlib)
~~~

*   Import specific items from a library to shorten programs.
*   Use from...import... to load only specific items from a library.
*   Then refer to them directly without library name as prefix.

~~~
from pathlib import Path
metasearch_dir = Path('.').absolute()
print(metasearch_dir)
~~~

*   To build paths when the segments are not known in advance, use joinpath(), passing each path segment as a separate argument.

~~~
subdirs = ['crawler', 'metadata']
metadata_dir = metasearch_dir.joinpath(*subdirs)
print(metadata_dir)
~~~

*   Given an existing path object, it is easy to build a new one with minor differences such as referring to a different file in the same directory. Use `with_name()` to create a new path that replaces the name portion of a path with a different file name. Use `with_suffix()` to create a new path that replaces the file name’s extension with a different value.

~~~
crawler_dir = metasearch_dir.joinpath('crawler')
py = crawler_dir.with_name('transform.py')
print(py)

ipynb = py.with_suffix('.ipynb')
print(ipynb)
~~~

*   Create an alias for a library when importing it to shorten programs.
*   Use import...as... to give a library a short alias while importing it.
*   Then refer to items in the library using that shortened name.

~~~
import pathlib as p
~~~

*   Commonly used for libraries that are frequently used or have long names.
*   E.g., matplotlib plotting library is often aliased as mpl.
*   But can make programs harder to understand, since readers must learn your program’s aliases.

*   Use `glob()` to find only files matching a pattern.

~~~
some_dir_with_csv = metasearch_dir.joinpath('crawler', 'clean-csv').resolve()
%cd $some_dir_with_csv
for f in some_dir_with_csv.glob('*.csv'):
    print(f)
    ~~~

*   The glob processor supports recursive scanning using the pattern prefix ** or by calling `rglob()` instead of `glob()`. Multiple wildcards can be passed to glob methods.

~~~
for f in metasearch_dir.rglob('*-*.csv'):
    print(f)
    ~~~

## Reading and Writing Files

*   Each Path instance includes methods for working with the contents of the file to which it refers. For immediately retrieving the contents, use `read_bytes()` or `read_text()`. Use the `open()` method to open the file and retain the file handle, instead of passing the name to the built-in `open()` function.

~~~
some_csvs = [x for x in metasearch_dir.rglob('*-*.csv')]
some_csv = some_csvs[0]
with some_csv.open('r', encoding='utf-8') as handle:
    print('read from open(): {!r}'.format(handle.read()))

print('read_text(): {!r}'.format(f.read_text('utf-8')))
~~~

*   To write to the file, use `write_bytes()` or `write_text()`.

~~~
f = metasearch_dir.joinpath('example.txt')
f.write_bytes('This is the content'.encode('utf-8'))
~~~

*   This will create the file if it does not exist and overwrite exiting content if it does.

~~~
%cat $metasearch_dir/ex*
~~~

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

## Deleting

*   For testing if a particular Path object corresponds to an actual file use `exists()`.
*   For removing files use unlink().

~~~
print('exists before removing:', f.exists())
f.unlink()
print('exists after removing:', f.exists())
~~~






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
