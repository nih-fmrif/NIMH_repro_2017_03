---
title: Versioning edits with Git
teaching: 30
exercises: 5
questions:
- "How do I record changes in Git?"
- "How do I record notes about what changes I made and why?"
objectives:
- "Go through the modify-add-commit cycle for one or more files."
- "Explain where information is stored at each stage of Git commit workflow."
keypoints:
- "Files can be stored in a project's working directory (which users see), the staging area (where the next commit is being built up) and the local repository (where commits are permanently recorded)."
- "`git add` puts files in the staging area."
- "`git commit` saves the staged content as a new commit in the local repository."
- "Always write a log message when committing changes."
- "View previous commits using the "git log" command."

---

We can check the contents of the file that we previously saved in our project directory using the `%cat` magic:
~~~
%cat metasearch_analysis.py
~~~
{: .source}

~~~
# coding: utf-8
# get_ipython().system('git clone https://github.com/OpenNeuroLab/metasearch.git')
~~~
{: .output}


As we saw previously the status of our git repository shows us that we have
this untracked file along with our directory with data:
~~~
!git status
~~~
{: .source}

~~~
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        metasearch/
        metasearch_analysis.py

nothing added to commit but untracked files present (use "git add" to track)
~~~
{: .output}

The first step in tracking a file in Git is to add it to the Git staging area.

![The file lifecycle in git](../fig/git_add.png)
Modified figure from git-scm.com


In order to add a file to the Git staging area we use "git add":

~~~
!git add metasearch_analysis.py
~~~
{: .source}

We check how this changed the way Git see our current project with the "git status" command once again:

~~~
!git status
~~~
{: .source}

~~~
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   metasearch_analysis.py

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        metasearch/

~~~
{: .output}

Git now knows that it's supposed to keep track of `metasearch_analysis.py`, but
it hasn't recorded these changes permanently in its repository yet. To
permanently store the current state of the metasearch_analysis.py file in the
Git repository we need to commit the changes that are staged. We use the `git
commit` command for this:

~~~
!git commit -m "add script for our analysis"
~~~
{: .source}

~~~
[master (root-commit) 0c89fa2] add script for our analysis
 1 file changed, 2 insertions(+)
 create mode 100644 metasearch_analysis.py
~~~
{: .output}

When we run "git commit", Git takes everything we have told it to save by using
"git add" and stores a copy permanently inside the special `.git` directory.
This permanent copy is called a [commit]({{ page.root }}/reference/#commit) (or
[revision]({{ page.root }}/reference/#revision)) and its short identifier is
`0c89fa2` (Your commit may have another identifier.)

We use the `-m` flag (for "message") to record a short, descriptive, and
specific comment that will help us remember later on what we did and why. If we
just run "git commit" without the `-m` option, Git will launch `atom` (or
whatever other editor we configured as `core.editor`) so that we can write a
longer message.

[Good commit messages][commit-messages] start with a brief (<50 characters) summary of
changes made in the commit.  If you want to go into more detail, add
a blank line between the summary line and your additional notes.

Now when we run "git status" we see:

~~~
!git status
~~~
{: .source}

~~~
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        metasearch/

nothing added to commit but untracked files present (use "git add" to track)
~~~
{: .output}

Not only is the metasearch_analysis.py file now tracked but it is also
no longer part of the output of  "git status". It is now in the unmodified
state. When we look at our repository's history we can observe our commit. For
this, we use "git log":

~~~
!git log
~~~
{: .source}

~~~
commit 0c89fa2638154272519761de68189f8bb0d0b789
Author: XXX <XXX@hotmail.com>
Date:   Mon Feb 27 16:12:08 2012 -0500

    add script for our analysis
~~~
{: .output}

"git log" lists all commits  made to a repository in reverse chronological
order. The listing for each commit includes the commit's full identifier (which
starts with the same characters as the short identifier printed by the `git
commit` command earlier), the commit's author, when it was created, and the log
message Git was given when the commit was created.

## Where Are My Changes?
If we run `%ls` at this point, we will see that there has been no obvious change
to the filesystem:

~~~
%ls
~~~
{: .source}

~~~
metasearch/ metasearch_analysis.py
~~~
{: .output}

There are no obvious changes observed in the project directory because Git
saves information about files' history in the special `.git` directory
mentioned earlier so that our filesystem doesn't become cluttered (and so that
we can't accidentally edit or delete an old version).
  
## The Git Lifecycle


We have now seen the different states that files typically inhabit as Git
tracks them. The default file state is unmodified. Any time we make a change to
any of our files tracked by Git we will observe that they are listed as
modified. We must stage and then commit such changes to return the files to
their unmodified state.

The cycle of making changes to files, staging these changes, and then committing them is continually repeated
and our project continues to develop with each file being represented in the
Git repository as a combination of committed changes. We will start
working through such a cycle now by making another edit to our analysis script.
For now we'll just add a comment to document the fact that we are using data
from the the Open Neuroimaging Laboratory at http://openneu.ro.

![The file lifecycle in git](../fig/git_workflow.png)
Figure from git-scm.com


>## Editing our script file
> If not already open in our text editor atom, we should now open it using the IPython `%edit` magic:
> ~~~
> %edit metasearch_analysis.py
> ~~~
> {: .source}
{: .callout}

Once we have finished editing our script we should observe something like the following:

~~~
%cat metasearch_analysis.py
~~~
{: .source}

~~~
# coding: utf-8
# Download the data from the Open Neuroimaging Labaroatory, see http://openneu.ro
# get_ipython().system('git clone https://github.com/OpenNeuroLab/metasearch.git')
~~~
{: .output}

At this point we will see that Git now views this as a modified file:

~~~
!git status
~~~
{: .source}

~~~
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   metasearch_analysis.py

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        metasearch/

no changes added to commit (use "git add" and/or "git commit -a")
~~~
{: .output}

We previously used "git add" to add an untracked file to the staging area. This
time we will use it to add a modified file to the staging area.

~~~
!git add metasearch_analysis.py
~~~
{: .source}

Finally to complete the Git life-cycle for this current change-set we will commit our staged changes:

~~~
!git commit -m "add comment about Open Neuroimaging Laboratory"
~~~
{: .source}

~~~
[master b7dfff7] add comment about Open Neuroimaging Laboratory
 1 file changed, 2 insertions(+), 1 deletion(-)
~~~
{: .output}

We can use the "git status" and "git log" commands to confirm that an
additional commit is stored in the Git repository and no staged or unstaged
changes exist for the file metasearch_analysis.py.





## What if I don't want Git to track some of my changes?
There are many reasons we might want git to overlook certain files or sub-directories in our project. One such case is if our data contains Personally identifiable information (PII). Git helps us to share our code. This is still difficult to do if the content tracking system we use for our code contains this PII. To help with this we could explicitly include a directory in which we will add such data so that we reduce the risk of accidentally tracking such content. Let's do that now and add our dataset to this so that we don't accidentally include things we don't want to:

~~~
mkdir data_not_in_repo
mv metasearch data_not_in_repo
~~~
{: .source}






## Places to Create Git Repositories

The following commands start a new project, `more_scripts`, within the
`reproducibility_course` project. Is this a sensible idea? What problems
might it cause?
~~~
%mkdir more_scripts    # make a sub-directory reproducibility_course/more_scripts
%cd more_scripts       # go into reproducibility_course/more_scripts
!git init       # make the more_scripts sub-directory a Git repository
~~~
{: .bash}

Why is it a bad idea to do this? (Notice here that the
`reproducibility_course` project could now track the entire `more_scripts`
repository.) How can we undo this "git init"?

  
Git repositories can interfere with each other if they are "nested" in the
directory of another: the outer repository will try to version-control the
inner repository. Therefore, it's best to create each new Git repository in a
separate directory. To be sure that there is no conflicting repository in the
directory, check the output of "git status". If it looks like the following,
you are good to go to create a new repository:
 
~~~
!git status
~~~
{: .bash}
~~~
fatal: Not a git repository (or any of the parent directories): .git
~~~
{: .output}
 
  
  


 <!-- Similarly, we can ignore (as discussed later) entire directories, such as the `moons` directory:
Note that we can track files in directories within a Git:
 -->








Now suppose Dracula adds more information to the file.
(Again, we'll edit with `nano` and then `cat` the file to show its contents;
you may use a different editor, and don't need to `cat`.)

~~~
!nano mars.txt
!cat mars.txt
~~~
{: .source}

~~~
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
~~~
{: .output}

When we run "git status" now,
it tells us that a file it already knows about has been modified:

~~~
!git status
~~~
{: .source}

~~~
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   mars.txt

no changes added to commit (use "git add" and/or "git commit -a")
~~~
{: .output}

The last line is the key phrase:
"no changes added to commit".
We have changed this file,
but we haven't told Git we will want to save those changes
(which we do with "git add")
nor have we saved them (which we do with "git commit").
So let's do that now. It is good practice to always review
our changes before saving them. We do this using "git diff".
This shows us the differences between the current state
of the file and the most recently saved version:

~~~
!git diff
~~~
{: .source}

~~~
diff --git a/mars.txt b/mars.txt
index df0654a..315bf3a 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,2 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
~~~
{: .output}

The output is cryptic because
it is actually a series of commands for tools like editors and `patch`
telling them how to reconstruct one file given the other.
If we break it down into pieces:

1.  The first line tells us that Git is producing output similar to the Unix `diff` command
    comparing the old and new versions of the file.
2.  The second line tells exactly which versions of the file
    Git is comparing;
    `df0654a` and `315bf3a` are unique computer-generated labels for those versions.
3.  The third and fourth lines once again show the name of the file being changed.
4.  The remaining lines are the most interesting, they show us the actual differences
    and the lines on which they occur.
    In particular,
    the `+` marker in the first column shows where we added a line.

After reviewing our change, it's time to commit it:

~~~
!git commit -m "Add concerns about effects of Mars' moons on Wolfman"
!git status
~~~
{: .source}

~~~
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   mars.txt

no changes added to commit (use "git add" and/or "git commit -a")
~~~
{: .output}

Whoops:
Git won't commit because we didn't use "git add" first.
Let's fix that:

~~~
!git add mars.txt
!git commit -m "Add concerns about effects of Mars' moons on Wolfman"
~~~
{: .source}

~~~
[master 34961b1] Add concerns about effects of Mars' moons on Wolfman
 1 file changed, 1 insertion(+)
~~~
{: .output}

Git insists that we add files to the set we want to commit
before actually committing anything. This allows us to commit our
changes in stages and capture changes in logical portions rather than
only large batches.
For example,
suppose we're adding a few citations to our supervisor's work
to our thesis.
We might want to commit those additions,
and the corresponding addition to the bibliography,
but *not* commit the work we're doing on the conclusion
(which we haven't finished yet).

To allow for this,
Git has a special *staging area*
where it keeps track of things that have been added to
the current [change set]({{ page.root }}/reference/#change-set)
but not yet committed.

> ## Staging Area
>
> If you think of Git as taking snapshots of changes over the life of a project,
> "git add" specifies *what* will go in a snapshot
> (putting things in the staging area),
> and "git commit" then *actually takes* the snapshot, and
> makes a permanent record of it (as a commit).
> If you don't have anything staged when you type "git commit",
> Git will prompt you to use "git commit -a" or "git commit --all",
> which is kind of like gathering *everyone* for the picture!
> However, it's almost always better to
> explicitly add things to the staging area, because you might
> commit changes you forgot you made. (Going back to snapshots,
> you might get the extra with incomplete makeup walking on
> the stage for the snapshot because you used `-a`!)
> Try to stage things manually,
> or you might find yourself searching for "git undo commit" more
> than you would like!
{: .callout}

![The Git Staging Area](../fig/fig/git-staging-area.svg)

Let's watch   as our changes to a file move from our editor
to the staging area
and into long-term storage.
First,
we'll add another line to the file:

~~~
!nano mars.txt
!cat mars.txt
~~~
{: .source}

~~~
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
~~~
{: .output}

~~~
!git diff
~~~
{: .source}

~~~
diff --git a/mars.txt b/mars.txt
index 315bf3a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite color
 The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
~~~
{: .output}

So far, so good:
we've added one line to the end of the file
(shown with a `+` in the first column).
Now let's put that change in the staging area
and see what "git diff" reports:

~~~
!git add mars.txt
!git diff
~~~
{: .source}

There is no output:
as far as Git can tell,
there's no difference between what it's been asked to save permanently
and what's currently in the directory.
However,
if we do this:

~~~
!git diff --staged
~~~
{: .source}

~~~
diff --git a/mars.txt b/mars.txt
index 315bf3a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite color
 The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
~~~
{: .output}

it shows us the difference between
the last committed change
and what's in the staging area.
Let's save our changes:

~~~
!git commit -m "Discuss concerns about Mars' climate for Mummy"
~~~
{: .source}

~~~
[master 005937f] Discuss concerns about Mars' climate for Mummy
 1 file changed, 1 insertion(+)
~~~
{: .output}

check our status:

~~~
!git status
~~~
{: .source}

~~~
On branch master
nothing to commit, working directory clean
~~~
{: .output}

and look at the history of what we've done so far:

~~~
!git log
~~~
{: .source}

~~~
commit 005937fbe2a98fb83f0ade869025dc2636b4dad5
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 10:14:07 2013 -0400

    Discuss concerns about Mars' climate for Mummy

commit 34961b159c27df3b475cfe4415d94a6d1fcd064d
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 10:07:21 2013 -0400

    Add concerns about effects of Mars' moons on Wolfman

commit f22b25e3233b4645dabd0d81e651fe074bd8e73b
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 09:51:46 2013 -0400

    Start notes on Mars as a base
~~~
{: .output}

> ## Paging the Log
>
> When the output of "git log" is too long to fit in your screen,
> `git` uses a program to split it into pages of the size of your screen.
> When this "pager" is called, you will notice that the last line in your
> screen is a `:`, instead of your usual prompt.
>
> *   To get out of the pager, press `q`.
> *   To move to the next page, press the space bar.
> *   To search for `some_word` in all pages, type `/some_word`
>     and navigate throught matches pressing `n`.
{: .callout}

> ## Limit Log Size
>
> To avoid that "git log" cover all your terminal screen you can
> limit the numbers of commit that Git will list by using `-N`
> where `N` is the number of commits that you want to receive
> the information. For example, if you only want the information
> from the last commit you can use
>
> ~~~
> !git log -1
> ~~~
> {: .source}
> 
> ~~~
> commit 005937fbe2a98fb83f0ade869025dc2636b4dad5
> Author: Vlad Dracula <vlad@tran.sylvan.ia>
> Date:   Thu Aug 22 10:14:07 2013 -0400
>
>    Discuss concerns about Mars' climate for Mummy
> ~~~
> {: .output}
>
> You can also reduce the quantity of information using the
> `--oneline` option:
>
> ~~~
> !git log --oneline
> ~~~
> {: .source}
> ~~~
> * 005937f Thoughts about the climate
> * 34961b1 Concerns about Mars's moons on my furry friend
> * f22b25e Starting to think about Mars
> ~~~
> {: .output}
>
> You can also combine the `--oneline` options with others. One useful
> combination is
>
> ~~~
> !git log --oneline --graph --all --decorate
> ~~~
> {: .source}
> ~~~
> * 005937f Thoughts about the climate (HEAD, master)
> * 34961b1 Concerns about Mars's moons on my furry friend
> * f22b25e Starting to think about Mars
> ~~~
> {: .output}
{: .callout}

To recap, when we want to add changes to our repository,
we first need to add the changed files to the staging area
("git add") and then commit the staged changes to the
repository ("git commit"):

![The Git Commit Workflow](../fig/fig/git-committing.svg)

> ## Choosing a Commit Message
>
> Which of the following commit messages would be most appropriate for the
> last commit made to `mars.txt`?
>
> 1. "Changes"
> 2. "Added line 'But the Mummy will appreciate the lack of humidity' to mars.txt"
> 3. "Discuss effects of Mars' climate on the Mummy"
>
> > ## Solution
> > Answer 1 is not descriptive enough,
> > and answer 2 is too descriptive and redundant,
> > but answer 3 is good: short but descriptive.
> {: .solution}
{: .challenge}

> ## Committing Changes to Git
>
> Which command(s) below would save the changes of `myfile.txt`
> to my local Git repository?
>
> 1. `!git commit -m "my recent changes"`
>
> 2. `!git init myfile.txt`  
>    `!git commit -m "my recent changes"`
>
> 3. `!git add myfile.txt`  
>    `!git commit -m "my recent changes"`
>
> 4. `!git commit -m myfile.txt "my recent changes"`
>
> > ## Solution
> >
> > 1. Would only create a commit if files have already been staged.
> > 2. Would try to create a new repository.
> > 3. Is correct: first add the file to the staging area, then commit.
> > 4. Would try to commit a file "my recent changes" with the message myfile.txt.
> {: .solution}
{: .challenge}

> ## Committing Multiple Files
>
> The staging area can hold changes from any number of files
> that you want to commit as a single snapshot.
>
> 1. Add some text to `mars.txt` noting your decision
> to consider Venus as a base
> 2. Create a new file `venus.txt` with your initial thoughts
> about Venus as a base for you and your friends
> 3. Add changes from both files to the staging area,
> and commit those changes.
>
> > ## Solution
> >
> > First we make our changes to the `mars.txt` and `venus.txt` files:
> > ~~~
> > !nano mars.txt
> > !cat mars.txt
> > ~~~
> > {: .source}
> > ~~~
> > Maybe I should start with a base on Venus.
> > ~~~
> > {: .output}
> > ~~~
> > !nano venus.txt
> > !cat venus.txt
> > ~~~
> > {: .source}
> > ~~~
> > Venus is a nice planet and I definitely should consider it as a base.
> > ~~~
> > {: .output}
> > Now you can add both files to the staging area. We can do that in one line:
> >
> > ~~~
> > !git add mars.txt venus.txt
> > ~~~
> > {: .source}
> > Or with multiple commands:
> > ~~~
> > !git add mars.txt
> > !git add venus.txt
> > ~~~
> > {: .source}
> > Now the files are ready to commit. You can check that using "git status". If you are ready to commit use:
> > ~~~
> > !git commit -m "Wrote down my plans to start a base on Venus"
> > ~~~
> > {: .source}
> > ~~~
> > [master cc127c2]
> > Wrote down my plans to start a base on venus
> > 2 files changed, 2 insertions(+)
> > ~~~
> > {: .output}
> > ~~~
> {: .solution}
{: .challenge}

> ## Author and Committer
>
> For each of the commits you have done, Git stored your name twice.
> You are named as the author and as the committer. You can observe
> that by telling Git to show you more information about your last
> commits:
>
> ~~~
> !git log --format=full
> ~~~
> {: .source}
>
> When commiting you can name someone else as the author:
>
> ~~~
> !git commit --author="Vlad Dracula <vlad@tran.sylvan.ia>"
> ~~~
> {: .source}
>
> Create a new repository and create two commits: one without the
> `--author` option and one by naming a colleague of yours as the
> author. Run "git log" and "git log --format=full". Think about ways
> how that can allow you to collaborate with your colleagues.
>
> > ## Solution
> >
> > ~~~
> > !git add me.txt
> > !git commit -m "Updated Vlad's bio." --author="Frank N. Stein <franky@monster.com>"
> > ~~~
> > {: .source}
> > ~~~
> > [master 4162a51] Updated Vlad's bio.
> > Author: Frank N. Stein <franky@monster.com>
> > 1 file changed, 2 insertions(+), 2 deletions(-)
> >
> > !git log --format=full
> > commit 4162a51b273ba799a9d395dd70c45d96dba4e2ff
> > Author: Frank N. Stein <franky@monster.com>
> > Commit: Vlad Dracula <vlad@tran.sylvan.ia>
> >
> > Updated Vlad's bio.
> >
> > commit aaa3271e5e26f75f11892718e83a3e2743fab8ea
> > Author: Vlad Dracula <vlad@tran.sylvan.ia>
> > Commit: Vlad Dracula <vlad@tran.sylvan.ia>
> >
> > Vlad's initial bio.
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

[commit-messages]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
