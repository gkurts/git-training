# Git Basics - Saving and Inspecting

This section will cover some of most basic git commands, ones that that
anyone using git should know, and will be the most frequently used
commands regardless of the workflow you chose to use with git.

To demonstrate the usage of these commands, I will be working on a
sample project (add url), to help demonstrate how these commands
interact with your working environment

Commands covered:

- Initializing a git repository - git init
- Adding files to the staging area - git add
- Committing files to the git history - git commit
- Inspecting a repository - git status, git log

`git init`
----------

Start tracking a project in Git.

This command creates the .git directory. Most workflows typically have the repository created on your git host such as GitHub, GitLab, etc and you would clone it.

`git add`
---------

Git add will take a snapshot of the file and add it to the staging area.

If further changes are made to a file,  you will need to add the file
again for it to be included in the next commit.

- `git add <file>` -- add a file to the staging area
- `git add -A` -- add changes from all untracked files
- `git add -u` -- update tracked files

`git status`
------------

Git status will show you a status of your current working directory,
showing which files have been added, modified or untracked.

```
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

Looking at the output from this command, we can see that:

* slides.md is currently not being tracked
* client/index.html has been modified - and is not in staging
* newfile.md is staged and ready to be committed

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
at the time I did 'git add' is what would be committed.

Git now sees that there are unstaged changes. For these changes to be included in the next commit, I could:

* `git add newfile.md` --- re-add the one file
* `git add -u` - update all modified and tracked files files
* `git add -A` - add all files tracked and untracked


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

## Good Commits

![original](http://imgs.xkcd.com/comics/git_commit.png)
---

Do's
----
- keep commit changes as small as possible
- describe what was changed and why
- limit first line to 50 characters
- insert a blank line after first line
- wrap subsequent lines at 72 characters

Don'ts
------
- mix whitespace with functional code changes
- mix unrelated functional code changes
- send large feature in a single commit

Model Git commit message
------------------------

```
Capitalized, short (50 chars or less) summary

More detailed explanatory text, if necessary.  Wrap it to about 72
characters or so.  In some contexts, the first line is treated as the
subject of an email and the rest of the text as the body.  The blank
line separating the summary from the body is critical (unless you omit
the body entirely); tools like rebase can get confused if you run the
two together.

Write your commit message in the imperative: "Fix bug" and not "Fixed bug"
or "Fixes bug."  This convention matches up with commit messages generated
by commands like git merge and git revert.

Further paragraphs come after blank lines.

- Bullet points are okay, too

- Typically a hyphen or asterisk is used for the bullet, preceded by a
  single space, with blank lines in between, but conventions vary here

- Use a hanging indent
```

## `git commit --amend`

Add any staged changes to the last commit and amend the commit message (optional).

Useful for when you commit early and forget to add some files or when you make a mistake in the commit message.

## `git stash`

Save the uncommitted changes in the working directory and the staging area and go back to a clean working directory.


Git Log
-----

Git log is a powerful tool to look through the history of your repository. Many of the UI's for it will use the information of git log to drive the visualizations.

There is quite a bit of flexability with git log, but I will cover a few basics:

```
# commits in current branch
git log
# commits in another branch
git log branch
# commits in one branch but not in another
git log branch1..branch2
# short log - groups commit by author and 1st line of commit
gitshortlog
# last N commits
git log -3
# logs since yesterday
git log --after='yesterday'
# logs before a date
git log --before="2014-01-01"
# logs with a graph for current branch
git log --oneline --decorate --graph
# logs with a graph for all branches
git log --oneline --decorate --graph --all
# just getting fancy with log now
git log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
```
Displays the commit history of your current branch

Git Basics - Undoing
====================

Since git stores snapshots of everything locally, it makes it easier to
undo changes, or pull up files / versions of your project from a
different point in time. The most common commands that you will use for
working with your history are:

- git checkout
- git reset
- git revert

`git checkout`
--------------

Git checkout allows us to check out files, change sets or branches into
the current working directory. For undoing changes, we will focus on
checking out files, or files within a change set.

### quick undo


A useful way to use checkout is the command 'git checkout -- .', this
will revert all of your modified files to the latest commit in your
branch. This is useful if you had made a bunch of changes that you no
longer want, and don't want comitted.

{{example: --- open up a project, put a bunch of stuff into files, then
git checkout -- .}}

### undoing a single file

If you only want to undo changes to one file, instead of
`git checkout -- .`, you can provide a file name:

`git checkout -- newfile.md`

If you have a large amount of changes that have not yet been comitted,
be careful when using `git checkout -- .` as it could lead to the loss
of work.

`git revert`
------------

Usage:

`git revert <commit>`

Git revert will attempt to revert a previous commit by undoing the operation and making a new commit with the result. This prevents you from losing track of history which can be important, and helps make git revert a safer way of undoing changes.


```
# in server/index.js - change the static path to say 'badclient'
git commit -a -m 'making a bad change'
# in server/index.js - change port from 3000 to 4000
git commit -a -m 'changing port'
# we now want to revert badchange, but keep the port change
# see the recent commits
git reflog
git revert <commit>
```

If git is able to automatically revert the change without conflicts, it will prompt you for a commit message to show the revert. If there is an issue - you may need to manually fix the conflict, and then merge the results.


`git reset`
------

git reset acts as a bit of a permeant 'undo' and git, and if used incorrectly - could cause you to lose work. When compared to git revert, which allows you to select commits from any point in time - git reset can only work backwards from your current (head/commit?)


See also:

https://www.atlassian.com/git/tutorials/undoing-changes/git-reset

Whereas reverting is designed to safely undo a public commit, git reset is designed to undo local changes. Because of their distinct goals, the two commands are implemented differently: resetting completely removes a changeset, whereas reverting maintains the original changeset and uses a new commit to apply the undo.

reset example:
- create branch, reset-example
- in index/server.js  - add a function, commit, x2
- git reset head~2 --- unstaged, not committed - but still in working
- git reset head~2 -- hard --- changes get totally removed

# Git Basics - Collaboration

Since git stores everything locally, it is able to provide developers
with an isolated environment to work with. This also allows you to work
with Git even when you are not connected to a network - as most commands
operate locally - such as git init, add, commit, reset and revert.

At some point though if you are part of a team, you need to share your
changes and work with others and this section will cover the commands
that git provides to let you share and collaborate with others.

The commands that we will discuss are:

- git clone
- git branch
- git remote
- git fetch
- git pull
- git push


## `git clone`
-----------

Get a copy of an existing Git repository.

This command copies the .git directory of a remote Git repository to
your local disk and checks out a working copy of the latest version of
the default branch.

`git clone https://github.com/e-schultz/git-training-app.git`

If you do not specify a folder name to clone into, a 'git-training-app'
folder will be created. If you want to clone into a different folder,
`git clone url foldername`, or if you want to clone into your current
folder - 'git clone url .'.

By default, git add a remote for where you cloned this from called
'origin'

## `git branch`
-------

In some other source control systems like SVN - branching is considered a heavy operation, and should only be done for major long-term projects.

With Git, branches are much more light weight - and become an integral part of most Git workflows.

Usages:

```
# show local branches
git branch
# verbose information
git branch -v
# show remote branches
git branch -r
# create a new branch - does not switch to branch
git branch <new branch>
# delete a branch that has been merged
git branch -d <branch name>
# force delete a branch with unmerged changes
git branch -D <branch name>
```

When creating a branch like this, it will not track it on a remote, and will not switch you to the current branch. A short-cut to create a new branch and switch to it: `git checkout -b <branchname>`

Once you have changes in your branch that you want to push: `git push`, if your upstream is unaware of this branch you need to tell git what the upstream is:

`git push --set-upstream origin chore-show-branch`


If you have created a branch that does not have an origin set, you will to tell git where remote upstream is.

```
git branch <branch-name>
git checkout <branch-name>
git push -u origin <branch-name>
```

Force pushing
-------------

If you think as 'git pull' as merging remote changes into your local branch, git push is merging your local changes into a remote branch.

If your local history has been re-written or diverged and can not do a fast-forward merge, then git will reject the push.

Depending on the cause of this, you can either force a push - or pull, try and merge the changes/resolve conflicts and then push again.

A common scenario where you might want to force a push is if you have a rebase.

Scenario:

* done a bunch of commits
* pushed to a remote for review
* done more commits
* rebase from master to clean up commit history
* push again

Git would reject this change unless you specify the --force flag. It is important however to only do a force push on changes that other developers are not relying on yet.


## `git remote`
------------

Git remote allows you to create, view and share links with other
repositories. Remotes act as aliases to other repositories to let you
easily work with them by being able to request changes, push changes,
etc by short name.

Usage:
```
# list remotes
git remote
# verbose list remotes
git remote -v
```

> aside: Forking
If you want to work on a repository that you are not a collaborator on, you will need to fork the repository to have your own copy.

When doing this, Git will automatically add an 'origin' remote which will point to your version of the repository. If you want to be able to keep in sync, and submit pull requests to the main repository - you will need to add an upstream remote.

```
git remote add https://github.com/e-schultz/git-training-app.git
```

## `git fetch`
-----------

Usage:
```
git fetch <remote>
git fetch <remote> <branch>
```

Fetch all of the branches from the remote repository. This also downloads all of the required commits and files from the other repository.

Doing a git fetch will not

## `git pull`
----

Usage:

```
git pull <remote>
```

Git pull will fetch the remote repository, and merge it. You can also do a rebase instead of a merge with the usage:

```
git pull --rebase <remote>
```

# git fetch vs git pull

The primary difference between git fetch and git pull, is that git pull will fetch the changes then merge then into your current branch. Git fetch will just get the changes, but will not merge them yet.

`git push`
--------

Usage:

```
# push a branch to the remote
git push <remote> <branch>
# force a push even if it's not a fast-forward merge
git push <remote> --force
# push all local branches
git push remote --all
```

## .gitignore

.gitignore is a simple text file that tells git what files and/or paths should not be tracked. When doing commands like git add, git status, etc files and paths in the .gitignore will not be included.

It is generally considered good practice not to include files managed by package mangers like node_modules for npm packages, or bower_components for bower.

It is also a good idea not to commit artifacts that are generated as part of a build process. Github has a collection of sample .gitignore files for many different enviroments/setups located [here](https://github.com/github/gitignore)

An example ignore file:

```
# Logs
logs
*.log

# Runtime data
pids
*.pid
*.seed

# Directory for instrumented libs generated by jscoverage/JSCover
lib-cov

# Coverage directory used by tools like istanbul
coverage

# Grunt intermediate storage (http://gruntjs.com/creating-plugins#storing-task-files)
.grunt

# Compiled binary addons (http://nodejs.org/api/addons.html)
build/Release

# Dependency directory
# Commenting this out is preferred by some people, see
# https://www.npmjs.org/doc/misc/npm-faq.html#should-i-check-my-node_modules-folder-into-git-
node_modules

# Users Environment Variables
.lock-wscript
```