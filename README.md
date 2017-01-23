NIMH course for reproducibility in neuroimaging.
==========================
Links :

Course info : [site](https://nih-fmrif.github.io/2017-03-13-nimh) and [github repository](https://github.com/nih-fmrif/2017-03-13-nimh)

Day 1 : [site](https://nih-fmrif.github.io/reproducibility_course_day_1) and [github repository](https://github.com/nih-fmrif/reproducibility_course_day_1)

Day 2 : [site](https://nih-fmrif.github.io/reproducibility_course_day_2) and [github repository](https://github.com/nih-fmrif/reproducibility_course_day_2)

Day 3 : [site](https://nih-fmrif.github.io/reproducibility_course_day_3) and [github repository](https://github.com/nih-fmrif/reproducibility_course_day_3)

Day 4 : [site](https://nih-fmrif.github.io/reproducibility_course_day_4) and [github repository](https://github.com/nih-fmrif/reproducibility_course_day_4) 


The course will:
+ Take place March 13th, and 15th-17th at NIH.
+ Draw heavily from the content of software/data carpentry
+ Similar to the carpentries it will put emphasis on hands-on acquisition of programming skills.
+ As with data carpentry it will maintain a single dataset throughout to give a sense of how all the tools tie together for an analysis.
+ Be divided into 4 days (described in more depth in [google doc](https://docs.google.com/document/d/1RtLaNrbFtXLmj53_dGmolqh0iGRxseQ5d6LkG-ojv28/edit?usp=sharing)):

### The course materials
The course materials are maintained in a similar manner to software carpentry from which we have imported this repository. A separate repository will be maintained for each day of the course.  Jekyll is used to render the repository as a website. So "nih-fmrif/reproducibility_course_day_1" will be hosted at https://nih-fmrif.github.io/reproducibility_course_day_1. Changes pushed to the repository will update the website. In order to push said changes, clone this repository, make your changes, and then push the changes back to the remote. The content for the main page is in index.md. The content for the individual lessons is in `_episodes/X.md`. Until the content has been edited it may bear no relation to the actual course material that day. We will use the  basic structure of the repository/website for convenience though. And there is some overlap in the material...


### Testing the website locally
If you want to generate the website locally for testing purposes there are guides on software carpentry linked below.

+ As described [here](https://swcarpentry.github.io/lesson-example/setup/) you will need ruby (with package manager npm) and jekyll (with kramdown), and python 3 with the pyyaml module installed.
+ You run`make serve` to serve the website locally and then point your browser to the appropriate port. 
+ More generally when you have make installed typing `make` in the base directory will provide a list of helpful commands.
+ If you're completely lost you can work you're way through [this](https://swcarpentry.github.io/lesson-example/) this description of how software carpentry lesson materials are created/maintained. 

