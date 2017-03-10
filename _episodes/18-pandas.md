---
title: "Pandas (template lesson)"
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

---


~~~
df_id = iris.groupby(iris['class'], as_index = False).count()
df_id = df_id.assign(id = range(1, 1 + len(df_id))).loc[:,['id','class']]
df_id
iris.merge(df_id, how = 'left', on = 'class')
~~~
{: .python}


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

