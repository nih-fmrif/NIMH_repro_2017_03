---
title: Introduction to Version Control and git
teaching: 10
exercises: 0
start: true
questions:
- "What is version control and why should I use it?"
- "How do I get set up to use Git?"
objectives:
- "Understand the benefits of an automated version control system."
- "Understand the basics of how Git works."
- "Configure `git` the first time it is used on a computer."
- "Understand the meaning of the `--global` configuration flag."
keypoints:
- "Version control is like an unlimited 'undo'."
- "Version control also allows many people to work in parallel."
-   "Use `git config` to configure a user name, email address, editor, and other preferences once per machine."
---

We'll start by exploring how version control can be used
to keep track of what one person did and when.
Even if you aren't collaborating with other people,
automated version control is much better than this situation:

[![Piled Higher and Deeper by Jorge Cham, http://www.phdcomics.com/comics/archive_print.php?comicid=1531](../fig/fig/phd101212s.png)](http://www.phdcomics.com)

"Piled Higher and Deeper" by Jorge Cham, http://www.phdcomics.com

We've all been in this situation before: it seems ridiculous to have
multiple nearly-identical versions of the same document. Some word
processors let us deal with this a little better, such as Microsoft
Word's "Track Changes" or Google Docs' [version
history](https://support.google.com/docs/answer/190843?hl=en).

Version control systems start with a base version of the document and
then save just the changes you made at each step of the way. You can
think of it as a tape: if you rewind the tape and start at the base
document, then you can play back each change and end up with your
latest version.

![Changes Are Saved Sequentially](../fig/fig/play-changes.svg)

Once you think of changes as separate from the document itself, you
can then think about "playing back" different sets of changes onto the
base document and getting different versions of the document. For
example, two users can make independent sets of changes based on the
same document.

![Different Versions Can be Saved](../fig/fig/versions.svg)

If there aren't conflicts, you can even play two sets of changes onto the same base document.

![Multiple Versions Can be Merged](../fig/fig/merge.svg)

A version control system is a tool that keeps track of these changes for us and
helps us version and merge our files. It allows you to
decide which changes make up the next version, called a
[commit]({{ page.root }}/reference/#commit), and keeps useful metadata about them. The
complete history of commits for a particular project and their metadata make up
a [repository]({{ page.root }}/reference/#repository). Repositories can be kept in sync
across different computers facilitating collaboration among different people.

> ## The Long History of Version Control Systems
>
> Automated version control systems are nothing new.
> Tools like RCS, CVS, or Subversion have been around since the early 1980s and are used by many large companies.
> However, many of these are now becoming considered as legacy systems due to various limitations in their capabilities.
> In particular, the more modern systems, such as Git and [Mercurial](http://swcarpentry.github.io/hg-novice/)
> are *distributed*, meaning that they do not need a centralized server to host the repository.
> These modern systems also include powerful merging tools that make it possible for multiple authors to work within
> the same files concurrently.
{: .callout}

> ## Paper Writing
>
> *   Imagine you drafted an excellent paragraph for a paper you are writing, but later ruin it. How would you retrieve
>     the *excellent* version of your conclusion? Is it even possible?
>
> *   Imagine you have 5 co-authors. How would you manage the changes and comments they make to your paper?
>     If you use LibreOffice Writer or Microsoft Word, what happens if you accept changes made using the
>     `Track Changes` option? Do you have a history of those changes?
{: .challenge}


## Setting up git
When we use Git on a new computer for the first time, we need to configure a
[few things](http://swcarpentry.github.io/git-novice/02-setup/). Below are a
few examples of configurations we will set as we get started with Git:

*   our name and email address,
*   to colorize our output,
*   what our preferred text editor is,
*   and that we want to use these settings globally (i.e. for every project)

On a command line, Git commands are written as `git verb`,
where `verb` is what we actually want to do. So we should type:

~~~
!git config --global user.name "our name"
!git config --global user.email "our email address"
!git config --global color.ui "auto"
!git config --global core.editor "atom --wait"
~~~
{: .source}

This user name and email will be associated with your subsequent Git activity,
which means that any changes pushed to [GitHub](http://github.com/),
[BitBucket](http://bitbucket.org/), [GitLab](http://gitlab.com/) or another Git
host server in a later lesson will include this information. If you are
concerned about privacy, please review GitHub's
[instructions](https://help.github.com/articles/keeping-your-email-address-private/)
 for keeping your email address private.


The four commands we just ran above only need to be run once: the flag `--global` tells Git
to use the settings for every project, in your user account, on this computer.

You can check your settings at any time:

~~~
!git config --list
~~~
{: .source}

You can reconfigure these settings whenever you wish.

> ## Proxy
>
> In some networks you need to use a
> [proxy](https://en.wikipedia.org/wiki/Proxy_server). If this is the case, you
> may also need to tell Git about the proxy:
>
> ~~~
> $ git config --global http.proxy proxy-url
> $ git config --global https.proxy proxy-url
> ~~~
> {: .bash}
>
> To disable the proxy, use
>
> ~~~
> $ git config --global --unset http.proxy
> $ git config --global --unset https.proxy
> ~~~
> {: .bash}
{: .callout}

> ## Git Help and Manual
>
> Always remember that if you forget a git command, you can access the list of command by using -h and access the git manual by using --help :
>
> ~~~
> $ git config -h
> $ git config --help
> ~~~
> {: .bash}
{: .callout}
