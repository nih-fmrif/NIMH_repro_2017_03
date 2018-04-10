NIMH course for reproducibility in neuroimaging.
==========================
Links :

Course materials site is rendered [here](https://nih-fmrif.github.io/NIMH_repro_2017_03).

NIMH's Data Science and Sharing Team will be conducting a workshop on open and
reproducible neuroscience the week of March 13th. Over the course of four
mornings (8:30a to 12:30p Mon, Wed, Thur, & Fri) we will provide hands on
training on:

- Using Python and Github to produce & share reproducible processing pipelines
- Structuring and reporting your data using community-recognized standards (COBIDAS, BIDS, EQUATOR)
- Accessing and contributing to share repositories
- Using pre-print servers (biorxiv.org)
- Accessing NIMH dedicated HPC resources

Mar 13, 15, 16, 17th, 8:30 am – 12:30 pm (Note Mar 14th is NIH Pi Day)

Note that space in the course is limited.  Our priority is to aim to maximize
the number of labs represents across the NIH Neuroscience Intramural Research
Program.

Course Organizers:
Peter Bandettini, SFIM, FMRIF
Adam Thomas, DSST, FMRIF
John Lee, DSST, FMRIF
Rick Reynolds, SSCC
Paul Taylor, SSCC
Sara Kimmich, SFIM
Matthew Brett


The course will:
+ Take place March 13th, and 15th-17th at NIH.
+ Draw heavily from the content of software/data carpentry
+ Similar to the carpentries it will put emphasis on hands-on acquisition of
  programming skills.
+ As with data carpentry it will maintain a single dataset throughout to give a
  sense of how all the tools tie together for an analysis.
+ Be divided into 4 days (described in more depth in [google
  doc](https://docs.google.com/document/d
  /1RtLaNrbFtXLmj53_dGmolqh0iGRxseQ5d6LkG-ojv28/edit?usp=sharing)):

### The course materials
The course materials are maintained in a similar manner to software carpentry
from which we have imported this repository. A separate repository will be
maintained for each day of the course.  Jekyll is used to render the repository
as a website. Changes pushed to the repository will update the website. In
order to push said changes, clone this repository, make your changes, and then
push the changes back to the remote. The content for the main page is in
index.md. The content for the individual lessons is in `_episodes/X.md`. Until
the content has been edited it may bear no relation to the actual course
material that day. We will use the  basic structure of the repository/website
for convenience though. And there is some overlap in the material...


### Testing the website locally
If you want to generate the website locally for testing purposes there are
guides on software carpentry linked below.

+ As described [here](https://swcarpentry.github.io/lesson-example/setup/) you
  will need ruby (with package manager npm) and jekyll (with kramdown), and
  python 3 with the pyyaml module installed.
+ You run`make serve` to serve the website locally and then point your browser
  to the appropriate port.
+ More generally when you have make installed typing `make` in the base
  directory will provide a list of helpful commands.
+ If you're completely lost you can work you're way through
  [this](https://swcarpentry.github.io/lesson-example/) this description of how
  software carpentry lesson materials are created/maintained.
+ Once setup the repository can generate a website locally. For example to host
  on localhost:11091 execute the command:
    
    jekyll serve --watch --port 11091& 


