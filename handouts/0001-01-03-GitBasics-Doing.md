Git Basics
==========

This section will cover some of the bread and butter commands that
anyone using git should know, and will be the most frequently used
commands regardless of the workflow you chose to use with git.

To demonstrate the usage of these commands, I will be working on a
sample project (add url), to help demonstrate how these commands
interact with your working environment

We will cover:

-   initializing a git repository - git init
-   adding files to the staging area - git add
-   committing files to the git history - git commit

`git init`
----------

Start tracking a project in Git.

This command creates the .git directory.

`git add`
---------

Git add will take a snapshot of the file and add it to the staging area.
The snapshot that is captured is the state of the file at the time that
you use this command. If you make further changes to a file that you
want to be captured in the next commit, you will need to add the file
again.

-   todo - expand
-   git add file
-   git add -a
-   git add -A
-   git add -u

`git status`
------------

Git status will show you a status of your current working directory,
showing which files have been added, modified or untracked.

``` {.bash}
On branch master
Your branch is ahead of 'origin/master' by 4 commits.
(use "git push" to publish your local commits)

Changes to be committed:
(use "git reset HEAD <file>..." to unstage)

new file:   newfile.md

Changes not staged for commit:
(use "git add <file>..." to update what will be committed)
(use "git checkout -- <file>..." to discard changes in working directory)

modified:   client/index.html

Untracked files:
(use "git add <file>..." to include in what will be committed)

slides.md
```

Looking at the output from this command, we can see that \* slides.md is
currently not being tracked \* client/index.html has been modified - and
is not in staging \* newfile.md is staged and ready to be comitted

If we make another change to newfile.md, the output from git status
looks like:

``` {.bash}
On branch master
Your branch is ahead of 'origin/master' by 4 commits.
(use "git push" to publish your local commits)

Changes to be committed:
(use "git reset HEAD <file>..." to unstage)

new file:   newfile.md

Changes not staged for commit:
(use "git add <file>..." to update what will be committed)
(use "git checkout -- <file>..." to discard changes in working directory)

modified:   client/index.html
modified:   newfile.md

Untracked files:
(use "git add <file>..." to include in what will be committed)

slides.md
```

New file is now listed as both a new file, and the contents of the file
at the time I did 'git add' is what would be committed, however Git now
sees that there are unstaged changes. To get these changes included in
my next commit I need to either add them with git add again, or use some
of the shortcuts available with git commit which will be discussed next.

`git commit`
------------

Git commit will move changes from the staging area to the history. An
important thing to note with git commit, is that the changes are only
committed locally - and not pushed to a server. This allows you to
commit early and often without worrying that other developers will be
pulling down incomplete changes.

The benefits of this include being able to adjust/revise your commits
before sending to the server, being able to try out new ideas - and easy
paths to revert / reset changes to get back to a previous state, or
simply being able to jump between tasks/branches and not lose your work
in progress.

In the previous example from git status, the only file that would be
part of the commit would be 'new file'. If you want to include all
staged files as part of the commit, you can use the shortcut
`git commit -a`

TODO: commit messages commit -m "message", editor for commits?

`git stash`
-----------

TODO: include git stash or not?
