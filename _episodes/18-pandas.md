---
title: "Pandas"
teaching: 20
exercises: 25
questions:
- ""
objectives:
- ""
- ""
keypoints:
- ""
- ""
- ""
- ""
- ""
---
---
title: "Pandas"
teaching: 10
exercises: 10
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
import pandas
~~~
{: .python}


One can access the values stored in a dataframe in many ways.

Three import components of the dataframe are the raw values, the column labels,
and the row labels. This can be accessed using the following attributes
respectively:
~~~
df_male_adult.values
df_male_adult.columns
df_male_adult.index
~~~
{: .python}
~~~
no output for now
~~~
{: .output}

To obtain subsets of these values we will look at four approaches. Integer based indexing, label based indexing, attribute based indexing, and dictionary based indexing. Using the iloc  for the
implicit indices of the dataframe include referring to the columns (as attributes of the
dataframe), loc for the explicit indices of the dataframe, and .


The columns can be accessed and used conveniently through the attributes of the dataframe:
~~~
df_male_adult.age
df_male_adult.age>50 # returns a pandas series object containing boolean values
~~~
{: .python}
~~~
no output for now
~~~
{: .output}


An equivalent syntax is to index the columns in the same way as a dictionary.
This takes more typing and impedes autocompletion:
~~~
df_male_adult['age']
df_male_adult['age']>50
~~~
{: .python}
~~~
no output for now
~~~
{: .output}

This alternative syntax has the advantage of not causing subtle bugs occurring
due to the fact that an attribute may have the same name as a method. This is
should be used for assigning values to new columns.
~~~
df_male_adult['age_in_ten_years'] = df_male_adult.age + 10
~~~
{: .python}
~~~
no output for now
~~~
{: .output}




`loc` is an indexer attribute. Like other attributes it is not a method so does
not use parentheses; however, it is different in that uses square brackets for
index in a similar manner to lists. Specifically the `loc` indexing attribute
allows us to access the explicitly defined labels for all columns and rows of
the dataframe.
~~~
# Selecting individual elements
df_male_adult.loc[8,'project']

# Specifying ranges 
df_male_adult.loc[0:8, 'project':'occupation']

# Selecting multiple rows using a list
df_male_adult.loc[[1,8,35],'project':'occupation']

# Using masking to select rows
df_male_adult.loc[[True,False,True,True,False],'age']

df_male_adult.loc[df_male_adult.loc[:,'age']>50, 'age']
~~~
{: .python}
~~~
no output for now
~~~
{: .output}

This seems awfully complicated to just get the rows where age is greater than 50. It is! We can do this far more easily by accessing the values in the age column by using the age attribute of the dataframe. Yes the column labels are stored as attributes.
~~~
df_male_adult.age
df_male_adult.age>50 # returns a pandas series object containing boolean values
~~~
{: .python}
~~~
no output for now
~~~
{: .output}

This results in a far more pleasant way to get all the rows are greater than 50:
~~~
df_male_adult.loc[df_male_adult.age>50, : ]
~~~
{: .python}
~~~
no output for now
~~~
{: .output}


Using the attributes to refer to columns comes with a caveat though. What
happens if we want to create a column called "shape". We already have an
attribute called shape. So we definitely don't want to use this approach when
assigning values for new columns. Instead we should take advantage of the
dictionary indexing approach. This approach treats a dataframe as a set of key
value pairs where each value is actually a column of values. So to create a new column called shape we would type:
~~~
df_male_adult.loc[df_male_adult.age>50, : ]
~~~
{: .python}
~~~
no output for now
~~~
{: .output}


Finally we may want to slice the rows by means other than comparison. We can
look through the methods to explore the various means of doing this
~~~
df_male_adult.loc[df_male_adult.age>50, : ]
~~~
{: .python}
~~~
no output for now
~~~
{: .output}




> ## Change me to a pandas exercise
>
> You want to select a random character from a string:
> ~~~
> bases = 'ACTTGCTTGAC'
> ~~~
>
> 1. What [standard library][stdlib] would you most expect to help?
> 2. Which function would you select from that library? Are there alternatives?
{: .challenge}

> ## Change me to a pandas exercise
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

> ## Change me to a pandas exercise
>
> 1. Fill in the blanks so that the program below prints `90.0`.
> 2. Rewrite the program so that it uses `import` *without* `as`.
> 3. Which form do you find easier to read?
>
> ~~~
> import math as m
> angle = ___.degrees(___.pi / 2)
> print(___)
> ~~~
> {: .python}
{: .challenge}

