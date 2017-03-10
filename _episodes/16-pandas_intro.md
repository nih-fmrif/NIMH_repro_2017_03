---
title: "Pandas intro and functions (template lesson)"
teaching: 15
exercises: 15
questions:
- "How can I create my own functions?"
objectives:
- "Explain and identify the difference between function definition and function call."
- "Write a function that takes a small, fixed number of arguments and produces a single result."
keypoints:
- "Break programs down into functions to make them easier to understand."
- "Define a function using `def` with a name, parameters, and a block of code."
- "Defining a function does not run it."
- "Arguments in call are matched to parameters in definition."
- "Functions may return a result to their caller using `return`."
---


~~~
import pandas as pd
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

## Break programs down into functions to make them easier to understand.

*   Human beings can only keep a few items in working memory at a time.
*   Understand larger/more complicated ideas by understanding and combining pieces.
    *   Components in a machine.
    *   Lemmas when proving theorems.
*   Functions serve the same purpose in programs.
    *   *Encapsulate* complexity so that we can treat it as a single "thing".
*   Also enables *re-use*.
    *   Write one time, use many times.

## Define a function using `def` with a name, parameters, and a block of code.

*   Begin the definition of a new function with `def`.
*   Followed by the name of the function.
    *   Must obey the same rules as variable names.
*   Then *parameters* in parentheses.
    *   Empty parentheses if the function doesn't take any inputs.
    *   We will discuss this in detail in a moment.
*   Then a colon.
*   Then an indented block of code.

~~~
def print_greeting():
    print('Hello!')
~~~
{: .python}

## Defining a function does not run it.

*   Defining a function does not run it.
    *   Like assigning a value to a variable.
*   Must call the function to execute the code it contains.

~~~
print_greeting()
~~~
{: .python}
~~~
Hello!
~~~
{: .output}

## Arguments in call are matched to parameters in definition.

*   Functions are most useful when they can operate on different data.
*   Specify *parameters* when defining a function.
    *   These become variables when the function is executed.
    *   Are assigned the arguments in the call (i.e., the values passed to the function).

~~~
def print_date(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)

print_date(1871, 3, 19)
~~~
{: .python}
~~~
1871/3/19
~~~
{: .output}

*   Via [Twitter](https://twitter.com/minisciencegirl/status/693486088963272705):
    `()` contains the ingredients for the function
    while the body contains the recipe.

## Functions may return a result to their caller using `return`.

*   Use `return ...` to give a value back to the caller.
*   May occur anywhere in the function.
*   But functions are easier to understand if `return` occurs:
    *   At the start to handle special cases.
    *   At the very end, with a final result.

~~~
def average(values):
    if len(values) == 0:
        return None
    return sum(values) / len(values)
~~~
{: .python}

~~~
a = average([1, 3, 4])
print('average of actual values:', a)
~~~
{: .python}
~~~
2.6666666666666665
~~~
{: .output}

~~~
print('average of empty list:', average([]))
~~~
{: .python}
~~~
None
~~~
{: .output}

*   Remember: [every function returns something]({{ page.root }}/04-built-in/).
*   A function that doesn't explicitly `return` a value automatically returns `None`.

~~~
result = print_date(1871, 3, 19)
print('result of call is:', result)
~~~
{: .python}
~~~
1871/3/19
result of call is: None
~~~
{: .output}

> ## Definition and Use
>
> What does the following program print?
>
> ~~~
> def report(pressure):
>     print('pressure is', pressure)
>
> print('calling', report, 22.5)
{: .challenge}

> ## Order of Operations
>
> The example above:
>
> ~~~
> result = print_date(1871, 3, 19)
> print('result of call is:', result)
> ~~~
> {: .python}
>
> printed:
> ~~~
> 1871/3/19
> result of call is: None
> ~~~
> {: .output}
>
> Explain why the two lines of output appeared in the order they did.
{: .challenge}

> ## Encapsulation
>
> Fill in the blanks to create a function that takes a single filename as an argument,
> loads the data in the file named by the argument,
> and returns the minimum value in that data.
>
> ~~~
> import pandas
>
> def min_in_data(____):
>     data = ____
>     return ____
> ~~~
> {: .python}
{: .challenge}

> ## Find the First
>
> Fill in the blanks to create a function that takes a list of numbers as an argument
> and returns the first negative value in the list.
> What does your function do if the list is empty?
>
> ~~~
> def first_negative(values):
>     for v in ____:
>         if ____:
>             return ____
> ~~~
> {: .python}
{: .challenge}

> ## Calling by Name
>
> What does this short program print?
>
> ~~~
> def print_date(year, month, day):
>     joined = str(year) + '/' + str(month) + '/' + str(day)
>     print(joined)
>
> print_date(day=1, month=2, year=2003)
> ~~~
> {: .python}
>
> 1.  When have you seen a function call like this before?
> 2.  When and why is it useful to call functions this way?
> {: .python}
{: .challenge}

> ## Encapsulating Data Analysis
>
> Assume that the following code has been executed:
>
> ~~~ 
> import pandas
>
> df = pandas.read_csv('gapminder_gdp_asia.csv', index_col=0)
> japan = df.ix['Japan']
> ~~~
> {: .python}
>
> 1. Complete the statements below to obtain the average GDP for Japan
>    across the years reported for the 1980s.
>
> ~~~ 
> year = 1983
> gdp_decade = 'gdpPercap_' + str(year // ____)
> avg = (japan.ix[gdp_decade + ___] + japan.ix[gdp_decade + ___]) / 2
> ~~~
> {: .python}
>
> 2. Abstract the code above into a single function.
>
> ~~~
> def avg_gdp_in_decade(country, continent, year):
>     df = pd.read_csv('gapminder_gdp_'+___+'.csv',delimiter=',',index_col=0)
>     ____
>     ____
>     ____
>     return avg
> ~~~
> {: .python}
>
> 3. How would you generalize this function
>    if you did not know beforehand which specific years occurred as columns in the data?
>    For instance, what if we also had data from years ending in 1 and 9 for each decade?
>    (Hint: use the columns to filter out the ones that correspond to the decade,
>    instead of enumerating them in the code.) 
>
> > ## Solution
> >
> > 1. 
> >
> > ~~~ 
> > year = 1983
> > gdp_decade = 'gdpPercap_' + str(year // 10)
> > avg = (japan.ix[gdp_decade + '2'] + japan.ix[gdp_decade + '7']) / 2
> > ~~~
> > {: .python}
> >
> > 2.
> >
> > ~~~
> > def avg_gdp_in_decade(country, continent, year):
> >     df = pd.read_csv('gapminder_gdp_' + continent + '.csv', index_col=0)
> >     c = df.ix[country]
> >     gdp_decade = 'gdpPercap_' + str(year // 10)
> >     avg = (c.ix[gdp_decade + '2'] + c.ix[gdp_decade + '7'])/2
> >     return avg
> > ~~~
> > {: .python}
> >
> > 3. We need to loop over the reported years
> >    to obtain the average for the relevant ones in the data.
> >
> > ~~~
> > def avg_gdp_in_decade(country, continent, year):
> >     df = pd.read_csv('gapminder_gdp_' + continent + '.csv', index_col=0)
> >     c = df.ix[country] 
> >     gdp_decade = 'gdpPercap_' + str(year // 10)
> >     total = 0.0
> >     num_years = 0
> >     for yr_header in c.index: # c's index contains reported years
> >         if yr_header.startswith(gdp_decade):
> >             total = total + c.ix[yr_header]
> >             num_years = num_years + 1
> >     return total/num_years
> > ~~~
> > {: .python}
> {: .solution}
{: .challenge}
