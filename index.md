name: inverse
layout: true
class: center, middle, inverse
---
#GIT

.footnote[Slides prepared by Kendall Blake]
---
## What is it and why should I be using it?
---
layout: false
.left-column[
  ## What is it?
]
.right-column[
  A distributed version control system!  Translated into English, that means
software which performs all the nasty bookkeeping parts of dealing with changes
in files.red[*] over time.


.footnote[.red[*] Actually, it could be any kind of data -- but we area mostly concerened with source code files]
]
---
.left-column[
  ## What is it?
  ## Why use it?
]
.right-column[
  .gray[A distributed version control system!  Translated into English, that means
software which performs all the nasty bookkeeping parts of dealing with changes
in files over time.]

Git gives you a safety net so that you can tinker and experiment without fear
of losing your work.  It is also a well-known and widely used system which
makes it easy to <a href="https://www.google.com/#q=site:stackoverflow.com+how+do+I+get+started+using+git">get good answers</a> about using it from people who do every day. 

]
---
template: inverse

## How does it work?
---
name: how

.left-column[
  ## How does it work?
  ### - Repositories
]
.right-column[
A git repository is the database where git stores all of its information about
the files which it is tracking.
]
---
.left-column[
  ## How does it work?
  ### - Repositories
  ### - Commits
]
.right-column[
The repository holds commits, which are groups of files with some additional
information, like:

- who made the commit

- a .keyphrase[commit message] explaining why the commit was made

- when the commit was made

- which commit came before that commit (the .keyphrase[parent])

Commits each have an ID called a .keyphrase[hash] which uniquely identifies them.
]
---
.left-column[
  ## How does it work?
  ### - Repositories
  ### - Commits
]
.right-column[
A commit might look something like this:
```
commit a2d90afd5f69ffb07fe3f053f1349e80a2c427fb
Author: Kendall Blake <kblake@bates.edu>
Date:   Fri Apr 22 11:12:11 2016 -0400

Print out a "Hello, World!" message.

```

```c
/* hello.c: */
#include <stdio.h>

int main (int argc, char *argv[])
{
	printf ("Hello, World!\n");
	return 0;
}
```
]
---
.left-column[
  ## How does it work?
  ### - Repositories
  ### - Commits
  ### - Branches
]
.right-column[
A .keyphrase[branch] is a line of commits.  A brand-new git repository will have
a single branch, named .keyphrase[master].  The custom among most git users is
to keep the master branch as the starting point for new work.

Often a programmer will create a new branch to work on each new piece of
functionality in a program.  This will allow the programmer to quickly abandon
ideas which are not working and more easily .keyphrase[merge] changes back into
master.
]
---
template: inverse

## Let's dive in!
---
.left-column[
  ## Init
  ### Github
]
.right-column[
Open the [GitHub Hello World](https://guides.github.com/activities/hello-world/) instructions in a new browser window.  I'll call this your .keyphrase["Instructions Window"]

Now open a second new window and navigate to the [GitHub home page](https://github.com).  Log in if necessary.  I'll call this your .keyphrase["GitHub Window"].

Scroll down to Step 1 in the Instructions Window, and follow those instructions to create your new git repository on github.
]
---
.left-column[
  ## Init
  ### Github
  ### Local
]
.right-column[
  ## First time setup

  Start > All Programs > Git > Git Bash

  ```bash
  $ git config --global --add user.name "Kendall Blake"
  $ git config --global --add user.email "kblake@bates.edu"
  $ git config --global --add core.editor "notepad"
  ```

  .red[You should put in your own information above, of course]

  ## Create a new repository

  ```bash
  $ git init hello-git
  ```

  ## Take a peek

  ```bash
  $ cd hello-git
  $ git status
  ```
]
???
  ### First time setup
  Before we dive in, lets put on our scuba gear.  We'll set up your identity
  and switch from the default editor to something that you'll likely be more
  comfortable using.  In the terminal commands that I write out below, I'll
  put in the initial $ that you'll see as your prompt.  When you enter in
  the commands, please only type the parts after the $.

  ### Create a new repository

  Now that git knows who you are, where to find you and how you like to write,
  we can get along with creating a new repository.  In your git bash window,
  go ahead and run the following command:

  ### Take peek

  That was easy!  Now you can move into that newly created directory and check
  the status of your git repository.
---
.left-column[
  ## Init
  ### Github
  ### Local
]
.right-column[
  ## Make sure you're where you want to be

  ```bash
  $ pwd
  ```

  ## Create your README file

  ```bash
  $ notepad README.
  ```

  ## Check the status of your work
  ```bash
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        README

nothing added to commit but untracked files present (use "git add" to track)

  ```

  
]
???
  ### Make sure you are where you want to be
  Now let's add a README file just like the github example.  First, make sure
  that you are still in your hello-git directory.

  You should see a path ending in "/hello-git". Mine says,
  "/c/Users/kblake/hello-git".  .red[Please stop me now if you don't think you are in your hello-git directory!]

  ### Create the readme
  Notepad will ask you if you want to create the file -- say "Yes."  Now write
  some words in that file, whatever you like.  Save the file (Ctrl+s) and exit
  notepad.  And yes, that dot at the end is there on purpose!

  Now run that git status command again.  This is an example of what you will
  see.  Use git status as often as you like.  Often it will point your way to
  the next action which you have to take.  Here, it tells us to use "git add"
  if we want to track an untracked file.

---
.left-column[
  ## Init
  ### Github
  ### Local
]
.right-column[
  ## Stage that README file

  ```bash
  $ git add README
  $ git status
  ```

  ## Commit it

  ```bash
  $ git commit
  $ git status
  ```

  ## Congratulations, you have a log:
  ```bash
$ git log
commit 4742b5d57736d563ec23075104fde95f721d7203
Author: Kendall Blake <kblake@bates.edu>
Date:   Tue Apr 26 14:21:38 2016 -0400

    Adding in a wonderful README file

  ```

  
]
???
  ### Stage
  Git turns the creation of a commit into a two-step process.  The first step
  gathers together all of the changes you want to make, and the second step
  stamps the commit and puts it into its proper place in the repository.  To
  compose the commit, we will use "git add".

  Also, please note that I have asked you to run "git status" after the add.
  You should see that the the README file is now listed under "changes to be
  committed."  Git status also tells you what to do if you made a mistake.

  ### Commit
  Notepad will come up.  Type in your commit message.  A good commit message
  will have:

 - An introductory headline (~80 characters)
 - A description of the reason for the change that this commit makes
 - A brief description of how this commit effects that change

  ### Log
  Git log shows you your history, commit-by-commit

---

.left-column[
  ## Branching
  ### GitHub
]
.right-column[
- Switch to the Instructions window
- Scroll down to Step 2
- Switch to the GitHub window and go to your hello-world repository
- Create the readme-edit branch
???
Now let's switch back to our Instructions Window and GitHub Window.  Scroll
down to Step 2.


]
---
.left-column[
  ## Branching
  ### Github
  ### Local
]
.right-column[
  ## Create a branch and then check it out

  ```bash
  $ git branch readme-edits
  $ git checkout readme-edits
  $ git status
  ```

  ## Look at branches

  ```bash
  $ git branch
  ```

]
???
  ### Branch
  On the command line, branching is also very easy - and fast.

  ### Look at branches
  You can "git checkout" any branches you see there, too

---

.left-column[
  ## Committing
  ### GitHub
]
.right-column[
- Switch to the Instructions window
- Scroll down to Step 3
- Switch to the GitHub window and go to your hello-world repository
- Edit your README.md
- Click Commit
???
Now let's switch back to our Instructions Window and GitHub Window.  Scroll
down to Step 3.

]
---
.left-column[
  ## Committing 
  ### Github
  ### Local
]
.right-column[
  ## Edit README file

  ```bash
  $ notepad README
  $ git status
  ```

  ## Stage it
  ```bash
  $ git add README
  $ git status
  ```

  ## Commit it

  ```bash
  $ git commit
  $ git status
  ```
]
???
  ### Committing
  I know what you're thinking: we've already done this!  Yes, we have.  And we
  might as well do it again and again and again.  If you continue to use 
  git, or any revision control system, you will do this again and again.

  If you look on your printout, you'll notice that I have a lovely example of
  what is colloquially referred to as "Programmer Art" - my diagram of the
  "Git Cycle."  Here it is, on this slide.

  You can think of the git cycle as being like a bicycle.  It goes round and
  round.  Each individual turn of the wheel doesn't get you very far, but if 
  you stick with it, you won't notice each spin and those many cycles will take
  you a long way.

  I promise that's my last bicycle metaphor.

---

.left-column[
  ## Pull Requests
  ### GitHub
]
.right-column[
- Switch to the Instructions window
- Scroll down to Step 4
- Create a pull request and submit it!
???
Now let's switch back to our Instructions Window and GitHub Window.  Scroll
down to Step 4.

Pull requests are a distinctive component of GitHub.  Git supports many ways of
sending patches and change requests.  The original means was by formatting
individual patches which were sent over a mailing list.  Programmers write their
code and commit into a local repository, then use some git tooling to prepare
their commits to go out for review via email.

Other online git systems, like GitLab, have similar features to GitHub.  GitLab
calls their "Pull Requests" Merge requests.  If you've already wandered down to
Step 5 in the Instructions Window, you might get a sense why.



]
---

.left-column[
  ## Merging
  ### GitHub
]
.right-column[
- Switch to the Instructions window
- Scroll down to Step 5
- In the GitHub window, merge your pull request
???
This is the simplest case for merging, and "in the real world" not the one
which you'll worry about too much.

Fortunately, you'll probably only run into "the real world" if you use git
to work on group projects, or if you start trying to merge many branches
together without pre-planning.

]
---
.left-column[
  ## Merging
  ### GitHub
  ### Local
]
.right-column[
## Do a test merge first
- Check out your destination branch (master)
- Create a brand new branch (test-merge, perhaps?)
- Perform the merge!

```bash
$ git checkout master
$ git branch test-merge
$ git checkout test-merge
$ git merge readme-edit
```

## Now do it for real!

```bash
$ git checkout master
$ git merge readme-edit
```

## And clean up after ourselves

```bash
$ git branch -D test-merge
```
]
???

I always like to do test merges first.  Then I can work through any issues
without worrying about putting my master branch in a state where I can't
quickly switch focus and work on something else.  Git also has some support
for repeating merge resolutions that the user has worked out before.

I'm also pathologically lazy and can't be bothered to remember the syntax for
how to merge one branch into another when you don't have either checked out.
That's why I always just checkout the destination, and then it's easy: "git
merge <branch to merge in>"

### Testing

Here we are creating a new branch.  There's actually a shortcut for the two
commands of branching and then checking out a new branch: run "git checkout -b
new-branch-name".

### Doing it for real

One of the great things about computers is that they are very good with
repeating actions!

### Cleaning up

The -D flag to "git branch" instructs git to Delete the branch named.  This is
not actually as scary as it sounds - Git still has those commits in its
repository!

---
name: last-page
template: inverse

## Thanks!

You can get view these slides online at:  http://abacus.bates.edu/~kblake/dcs-git/

. . . and you can git clone them too!

```bash
$ git clone http://abacus.bates.edu/~kblake/dcs-git/
```


