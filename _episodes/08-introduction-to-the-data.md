---
title: "Introduction to the data"
teaching: 15
exercises: 10
questions:
- "Where can I get neuroimaging data"
- "What is FAIR data"
objectives:
- "Explore the data indexed by the MetaSearch component of OpenNeuroLab."
- "Explore how the data could be used."
- "Access the data programmatically."
keypoints:
- "OpenNeuroLab, among many other data sharing resources, has made many
thousands of brain volumes available for community use."
---

## Introduction to OpenNeuroLab

*   Go to `openneu.ro`
* Work through the metasearch tutorial.
* Talk about the data. Touch on:
    - Efficient ways of accessing the data.
    - The benefit of sharing resources like this.
    - Similar resources that exist.
    - FAIR data.
   
## Getting the data

~~~
!git clone https://github.com/OpenNeuroLab/metasearch.git
~~~
{: .source}

In order to work with the files we have downloaded we will learn about libraries
in python. In particular, the pathlib library is useful for our current purposes.

