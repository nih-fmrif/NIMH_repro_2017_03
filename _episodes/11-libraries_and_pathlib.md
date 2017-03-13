---
title: "Libraries and pathlib"
teaching: 15
exercises: 15
start: true
questions:
- "How can I use software that other people have written?"
- "How can I find out what that software does?"
objectives:
- "Explain what software libraries are and why programmers create and use them."
- "Write programs that import and use libraries from Python's standard package."
- "Find and read documentation for standard libraries interactively (in the interpreter) and online."
keypoints:
- "Most of the power of a programming language is in its libraries."
- "A program must import a package in order to use it."
- "Use `help` to find out more about a package's contents."
- "Import specific items from a package to shorten programs."
- "Create an alias for a package when importing it to shorten programs."
---

## Most of the power of a programming language is in its libraries.

*   Although *library* has no rigorously defined meaning it can be used to
    refer to is a bundle of software that can be re-used by others.
    *   May also contain data values (e.g., numerical constants).
    *   Library's contents are supposed to be related, but there's no way to enforce that.
*   Python's [standard library][stdlib] is installed with it.
*   In Python, modules  are files containing code that we may want to reuse in
    some way. A number of modules can be bundled together and form what is
    called a package. 
*   These packages can be managed by tools like conda and pip and repositories
    from which anyone can download software exist at conda-forge and
    [PyPI][pypi] respectively. (the Python Package Index).
* We can easily create our own modules so that we can re- use our code in many
  projects.
    * This is especially useful for re-using functions, which we will learn about later.

## A program must import a module in order to use it.

*   Use `import` to load the contents of a package into a program's memory.
*   Then refer to things from the package as `package_name.sub_module_name`.
    *   Python uses `.` to mean "part of".
    *   The item in the package may in turn be a sub package

~~~
import math
math.pi
~~~
{: .python}

~~~
3.141592653589793
~~~
{: .output}

~~~
math.cos(math.pi)
~~~
{: .python}

~~~
-1.0
~~~
{: .output}

*   Have to refer to each item with the package's name.
    *   `math.cos(pi)` won't work: the reference to `pi`
        doesn't somehow "inherit" the function's reference to `math`.

## Use `help` to find out more about a package's contents.

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

## Import specific items from a package to shorten programs.

*   Use `from...import...` to load only specific items from a package.
*   Then refer to them directly without package name as prefix.

~~~
from math import cos, pi
cos(pi)
~~~
{: .python}

~~~
-1.0
~~~
{: .output}

## Create an alias for a package when importing it to shorten programs.

*   Use `import...as...` to give a package a short *alias* while importing it.
*   Then refer to items in the package using that shortened name.

~~~
import math as m
m.cos(m.pi)
~~~
{: .python}

~~~
-1.0
~~~
{: .output}

*   Commonly used for libraries that are frequently used or have long names.
    *   E.g., Numpy numeric analysis package is often aliased to np. The pandas
        package for dataframes is often aliased to pd.
*   But can make programs harder to understand, since readers must learn your
    program's aliases.


## Working with the pathlib package
Since we have downloaded a lot of files as part of the metasearch repository we
would like to use a package that will allow us to work with these files more
efficiently. The pathlib package is ideal for this. Let's import from this to
start working with paths:

~~~
from pathlib import Path
~~~
{: .python}

*   We use the Path class in the pathlib package to create Path objects, which
    we can then use for subsequent processing. To create a new path object we
    provide a name as the first argument. This name is a string representation of a
    path. We will create a Path object that represents the directory we downloaded:

~~~
metasearch_dir = Path('metasearch')
metasearch_dir
~~~
{: .python}
~~~
metasearch
~~~
{: .output}

*   The `absolute()` method can be used to convert a relative path to an
    absolute path:

~~~
metasearch_dir.absolute()
~~~
{: .python}

~~~
/home/this_user/reproducibility_course/metasearch
~~~
{: .output}

## Data descriptors of a Path object

In addition to some convenient methods to work with filesystem paths the
metasearch_dir object has more useful things to help us when we work with
paths.  More specifically it has what are termed
https://docs.python.org/3/howto/descriptor.html. These are accessed in a
similar manner to the methods but without parentheses. As an example we'll use
the `parent` data descriptor:


~~~
metasearch_dir.parent
~~~
{: .python}

~~~
PosixPath('.')
~~~
{: .output}

In this case the descriptor is not particularly useful because metasearch_dir
is specified as a relative path. We can use the `absolute()` method to fix this:

~~~
metasearch_dir.absolute().parent
~~~
{: .python}

~~~
PosixPath('/home/this_user/reproducibility_course')
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
help for the Path class from the pathlib package:

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

##  Other useful methods for working with Path objects

Given an existing path object, it is easy to build a new one with minor
differences. For example, we can easily construct a path to a  different file
in the same directory by using the `with_name()` method. 

~~~
crawler_dir = metasearch_dir.joinpath('crawler')
py = crawler_dir.with_name('transform.py')
py
~~~
{: .python}

~~~
metasearch/transform.py
~~~
{: .output}

We can use the
`with_suffix()` method to create a new path that replaces the file name’s
extension with that of a different filetype.

~~~
ipynb = py.with_suffix('.ipynb')
ipynb
~~~
{: .python}

~~~
metasearch/transform.ipynb
~~~
{: .output}

*   Our metasearch_dir object includes a `resolve()` method for normalizing a
    path by looking at the filesystem for directories and producing the
    absolute path referred to by a name. Symbolic links will be resolved and on
    Windows slashes will be replaced with backslashes. Our path does not
    contain symbolic links and the resolved path is identical to the absolute
    path:

~~~
metasearch_dir.resolve()
~~~
{: .python}

~~~
/home/this_user/reproducibility_course/metasearch
~~~
{: .output}


## Constructing paths with multiple directory arguments

We can build up a path by providing directories to the joinpath(). We pass each
path segment as a separate argument:

~~~
metadata_dir = metasearch_dir.joinpath('crawler', 'metadata')
metadata_dir
~~~
{: .python}

~~~
metasearch/crawler/metadata
~~~
{: .output}

A more convenient way of passing a list as multiple arguments to a function is
to use the star operator to "unpack" them:

~~~
subdirs = ['crawler', 'metadata']
metadata_dir = metasearch_dir.joinpath(*subdirs)
metadata_dir
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
metadata_dir.exists()
~~~
{: .python}

~~~
True
~~~
{: .output} 



## Working with multiple Paths

*   Some methods of the Path object return contents of the directory as an
    iterable. Specifically it returns a generator. We can use a list
    comprehension, discussed previously, to retrieve all the files (and
    subdirectories) captured by the generator.

~~~
[x for x in crawler.iterdir()]
~~~
{: .python}

~~~
[PosixPath('metasearch/crawler/Load.ipynb'),
 PosixPath('metasearch/crawler/brain-development'),
 PosixPath('metasearch/crawler/brainbox-csv'),
 PosixPath('metasearch/crawler/clean-csv'),
 PosixPath('metasearch/crawler/dataverse'),
 PosixPath('metasearch/crawler/example_repository'),
 PosixPath('metasearch/crawler/fcp-indi.gz'),
 PosixPath('metasearch/crawler/fcp-indi'),
 PosixPath('metasearch/crawler/fcp-info.ipynb'),
 PosixPath('metasearch/crawler/ixi-crawl.ipynb'),
 PosixPath('metasearch/crawler/metadata'),
 PosixPath('metasearch/crawler/process-clean-csv.ipynb'),
 PosixPath('metasearch/crawler/process-csv.ipynb'),
 PosixPath('metasearch/crawler/transform.ipynb')]
 ~~~
{: .output}

*   If the Path does not refer to a directory, `iterdir()` raises
    NotADirectoryError.

We can be more selective in the contents that we return if we use the `glob()`
method. This method allows us to find only files matching a pattern. We'll try
to find files that end in "csv":


~~~
[f for f in crawler_dir.glob('*.csv')]
~~~
{: .python}

~~~
[]
~~~
{: .output}

We didn't find any csv files. There are some ipython notebooks in the current
directory though:

~~~
[x for x in crawler_dir.glob('*.ipynb')]
~~~
{: .python}

~~~
[PosixPath('metasearch/crawler/Load.ipynb'),
 PosixPath('metasearch/crawler/fcp-info.ipynb'),
 PosixPath('metasearch/crawler/ixi-crawl.ipynb'),
 PosixPath('metasearch/crawler/process-clean-csv.ipynb'),
 PosixPath('metasearch/crawler/process-csv.ipynb'),
 PosixPath('metasearch/crawler/transform.ipynb')]
~~~
{: .output}

*   The glob processor supports recursive scanning using the pattern prefix
    `**`. Multiple wildcards can be passed to glob methods.

~~~
[f for f in crawler_dir.glob('**/*-*.ipynb')]
~~~
{: .python}

~~~
[PosixPath('metasearch/crawler/fcp-info.ipynb'),
 PosixPath('metasearch/crawler/ixi-crawl.ipynb'),
 PosixPath('metasearch/crawler/process-clean-csv.ipynb'),
 PosixPath('metasearch/crawler/process-csv.ipynb'),
 PosixPath('metasearch/crawler/fcp-indi/fcp-indi-extractor.ipynb')]
~~~
{: .output}

We will be able to interpret the content from csv files more readily so we'll
recursively search for csv files in the crawler directory:

~~~
csvs = [f for f in crawler_dir.glob('**/*-*.csv')]
csvs
~~~
{: .python}

~~~
[PosixPath('metasearch/crawler/brainbox-csv/all-mris.csv'),
 PosixPath('metasearch/crawler/clean-csv/ABIDE_Initiative-clean.csv'),
 PosixPath('metasearch/crawler/clean-csv/ACPI-clean.csv'),
 PosixPath('metasearch/crawler/clean-csv/ADHD200-clean.csv'),
 PosixPath('metasearch/crawler/clean-csv/BrainGenomicsSuperstructProject-clean.csv'),
 PosixPath('metasearch/crawler/clean-csv/CORR-clean.csv'),
 PosixPath('metasearch/crawler/clean-csv/HypnosisBarrios-clean.csv'),
 PosixPath('metasearch/crawler/clean-csv/IXI-clean.csv'),
 PosixPath('metasearch/crawler/clean-csv/RocklandSample-clean.csv'),
 PosixPath('metasearch/crawler/clean-csv/all-session.csv'),
 PosixPath('metasearch/crawler/fcp-indi/rocklandsample/nki-rs_lite_r4_phenotypic_v1.csv'),
 PosixPath('metasearch/crawler/fcp-indi/rocklandsample/nki-rs_lite_r6_phenotypic_v1.csv'),
 PosixPath('metasearch/crawler/fcp-indi/rocklandsample/nki-rs_lite_r7_phenotypic_v1.csv'),
 PosixPath('metasearch/crawler/fcp-indi/rocklandsample/nki-rs_lite_r8_phenotypic_v1.csv')]
~~~
{: .output}



## Reading and Writing Files : File IO

*   Each Path instance includes methods for working with the contents of the
    file to which it refers. For immediately retrieving the contents, use
    `read_bytes()` or `read_text()`. 

~~~
test = csvs[0]
text_output = test.read_text()
# Length of output:  
len(text_output)
# The first 100 characters:  
text_output[0:100]

~~~
{: .python}

~~~
Length of output:  984535
https://s3.amazonaws.com/fcp-indi/data/Projects/ABIDE_Initiative/Outputs/freesurfer/5.1/Pitt_0050002
~~~
{: .output}

We can use the `open()` method if we wish to have more control over the reading
process. This can be helpful if we don't wish to read the entire contents of a
file into memory. When using this method we retain a file handle for subsequent
reading from or writing to the file:

~~~
with test.open('r', encoding='utf-8') as file_handle:
    print(file_handle.readlines(200))
~~~
{: .python}


~~~
['https://s3.amazonaws.com/fcp-indi/data/Projects/ABIDE_Initiative/Outputs/freesurfer/5.1/Pitt_0050002/mri/T1.mgz,50002,abide_initiative\n', 'https://s3.amazonaws.com/fcp-indi/data/Projects/ABIDE_Initiative/Outputs/freesurfer/5.1/Pitt_0050003/mri/T1.mgz,50003,abide_initiative\n']
~~~
{: .output}

*   To write to the file, use `write_text()` or `write_bytes()`. The
    `write_text()` method will create the file if it does not exist and
    overwrite exiting content if it does.

~~~
f = metasearch_dir.joinpath('example.txt')
f.write_text('This is the content'.encode('utf-8'))
~~~
{: .python}
 
We'll check that this worked by displaying the contents of all files with names
starting with "ex" in the metasearch directory:

~~~
%cat {metasearch_dir}/ex*
~~~
{: .python}

~~~
This is the content
~~~
{: .output}

> ## Getting help when using file IO operations
> 
> The pathlib package provides convenient access to some of python's built-in
> functions for reading and writing files. There is lots of useful help for
> these functions. 
> 
> As an example try:
> 
> ~~~
> help(open)
> ~~~
> {: .python}
{: .callout}


## Removing files from the filesystem

The unlink() method of the Path class allows us to delete files from our filesystem:

~~~
# exists before removing: 
f.exists()
f.unlink()
# exists after removing: 
f.exists()
~~~
{: .python}

> ## File Properties
> 
> *   Detailed information about a file can be accessed using the methods stat().
> 
> ~~~
> stat_info = metasearch_dir.stat()
> 
> import time
> print('{}:'.format(stat_info))
> print('  Size (kB)    :', stat_info.st_size)
> print('  Created      :', time.ctime(stat_info.st_ctime))
> print('  Last modified:', time.ctime(stat_info.st_mtime))
> print('  Last accessed:', time.ctime(stat_info.st_atime))
> ~~~
> {: .python}
> 
> ~~~
> os.stat_result(st_mode=16872, st_ino=173483174, st_dev=20, st_nlink=7,
> st_uid=37163, st_gid=37163, st_size=4096, st_atime=1488916170,
> st_mtime=1488907986, st_ctime=1488907986):
>  Size (kB)    : 4096
>  Created      : Tue Mar  7 12:33:06 2017
>  Last modified: Tue Mar  7 12:33:06 2017
>  Last accessed: Tue Mar  7 14:49:30 2017
>  ~~~
>  {: .output}
{: .callout}



> ## Locating the Right Package
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

> ## Path construction
> 
> Construct a Path object with the following list and the metasearch_dir as the
> parent directory. Does this path exist in the metasearch repository? If it
> such a path didn't exist how would we create it?
> 
>  path_elements = ['csv_repository', 'brains.csv']
>  
>> ## Solution
>> ~~~
>>  constructed_path = metasearch_dir.joinpath(*path_elements)
>>  print('The path constructed is ', constructed_path)
>>  print(constructed_path.exists())
>> ~~~
>> {: .python}
>> 
>> ~~~
>> The path constructed is  metasearch/csv_repository/brains.csv
>> False
>> ~~~
>> {: .output}
>> 
>> To construct this path we can use the method `touch()`; however since the
>> parent directory also doesn't exist we should create that first:
>> 
>> ~~~
>> constucted_path.parent.mkdir()
>> constructed_path.touch()
>> print(constructed_path.exists())
>> ~~~
>> {: .python}
>> 
>> ~~~
>> True
>> ~~~
>> {: .output}
>> 
> {: .solution}
{: .challenge}


> ## Find the movies
> 
> Find movies.csv in the download metasearch repository and create a Path
> object called movies with this path as its name. Check that you have done
> this correctly by confirming that the methods of the Path object are
> available for your movies variable.
> 
>> ## Solution
>> 
>> We can search for any movies.csv file by using the glob method of our
>> metasearch_dir Path object. We need to be careful to extract the Path object
>> returned. We can use a list comprehension to avoid working with the generator
>> iterable returned by `glob()` and we can index into the resulting list to
>> return the desired Path object:
>> 
>> ~~~
>> movies = [csv for csv in metasearch_dir.glob()][0]
>> print(movies)
>> ~~~
>> {: .python}
>> 
>> ~~~
>> metasearch/docs/lib/parcoords/examples/data/movies.csv
>> ~~~
>> {: .output}
>>  
> {: .solution}
{: .challenge}

> ## What's in a csv?
> 
> Edit the code below to read the first 2 lines of all.csv located somewhere in the
> metasearch file tree. Write the output text to a file with the path
> "metasearch/my_dir/exercise.txt" using the Path class methods (so do not
> use IPython magic commands for filesystem manipulation).
> 
> ~~~
> nlines = 5
> output = ''
> with path_object.open('r') as f:
>     for ii in range(nlines):
>         output += 'csv-file "{!s}" , line {!s} : {!s}'.format(path.stem, ii+1,f.readline())
> print(output)
> ~~~
> {: .output}
> 
> 
> 
> 
> 
> 
>> ## Solution
>> 
>> We'll first create a Path object with the name of our target file:
>> 
>> ~~~
>> csv_file = [csv for csv in metasearch_dir.glob('**/all.csv')][0]
>> print(csv_file.exists())
>> ~~~
>> {: .python}
>> 
>> ~~~
>> True
>> ~~~
>> {: .output}
>> 
>> Then we will create a Path object the name of our output file. Since the
>> parent directory of our target file does not exist we will create that too:
>> 
>> ~~~
>> target_file = Path('my_dir/exercise.txt')
>> target_file.parent.mkdir()
>> ~~~
>> {: .python}
>> 
>> Finally we will read the contents of our csv_file and write the contents to our target file:
>> 
>> 
>> 
>> 
>> 
>> 
>> 
>> 
>> ~~~
>> movies = [csv for csv in metasearch_dir.glob()][0]
>> print(movies)
>> ~~~
>> {: .python}
>> 
>> ~~~
>> metasearch/docs/lib/parcoords/examples/data/movies.csv
>> ~~~
>> {: .output}
>>  
> {: .solution}
{: .challenge}

[pypi]: https://pypi.python.org/pypi/
[stdlib]: https://docs.python.org/3/library/
