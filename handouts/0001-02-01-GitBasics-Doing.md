# Git Basics - Saving and Inspecting

{todo: cut this section?}
This section will cover some of the bread and butter commands that
anyone using git should know, and will be the most frequently used
commands regardless of the workflow you chose to use with git.

To demonstrate the usage of these commands, I will be working on a
sample project (add url), to help demonstrate how these commands
interact with your working environment
{/todo}

Commands covered:

- Initializing a git repository - git init
- Adding files to the staging area - git add
- Committing files to the git history - git commit
- Inspecting a repository - git status, git log

`git init`
----------

Start tracking a project in Git.

This command creates the .git directory.

`git add`
---------

Git add will take a snapshot of the file and add it to the staging area.

The snapshot that is captured is the state of the file at the time that
you use this command.

If further changes are made to a file,  you will need to add the file
again.

- `git add <file>` -- add a file to the staging area
- `git add -A` -- add changes from all untracked files
- `git add -u` -- update tracked files

`git status`
------------

Git status will show you a status of your current working directory,
showing which files have been added, modified or untracked.

{todo: don't have most of the below in handouts - walk through as demo?}
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

Usage:
```
# commit staged snapshot
git commit
# commit staged files + modified tracked files
git commit -a
# add a commit message
git commit -a -m "your commit message here"
```

Git commit moves files from the staging area to the git history. It is important to note that the commit is not available to other people yet, as commit is a local operation.

If the '-m' option is left out, a text editor will open allowing you to enter in a commit message.

`git commit --ammend`
----

Add any staged changes to the last commit and ammend the commit message (optional).

Useful for when you commit early and forget to add some files or when you make a mistake in the commit message.

`git stash`
-----------

TODO: include git stash or not?
