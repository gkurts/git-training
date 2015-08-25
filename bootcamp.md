* 1. [Understand Git's model.](#understanding-the-git-model)
* 2. [Always work on your private feature branch.](#always-work-on-your-private-feature-branch)
  * 2.1 [Work on your own fork.](#work-on-your-own-fork)
  * 2.2 [Give your branches sensible names.](#give-your-branches-sensible-names)
* 3. [Commit often](#commit-often).
* 4. [Stage selectively](#stage-selectively).
* 5. [Do not commit things that should be kept confidential](#do-not-commit-things-that-should-be-kept-confidential).
* 6. [Avoid committing generated artifacts.](#avoid-committing-generated-artifacts)
* 7. [Update and rebase often](#update-and-rebase-often).
* 8. [Use pull requests to integrate into upstream branch](#use-pull-requests-to-integrate-into-upstream-branch)
* 9. [Do not rewrite public history](#do-not-rewrite-public-history)
* 10. [Learn how to undo](#learn-how-to-undo)


# Intro

## About

This is an shortened version of our git-training course, with a focus on working with the Rangle Flow.
For more information, feel free to ask, and

* [Git Training Repository](https://github.com/rangle/git-training)
* [Rangle Flow Documentation](https://github.com/rangle/dev/tree/master/rangle-flow)

![inline](https://github.com/rangle/dev/blob/master/rangle-flow/rangle-flow.png)

## Useful Tools

* [GitX](http://gitx.frim.nl/)
* [Hub](https://github.com/github/hub) or [Git Extras](https://github.com/tj/git-extras)
* [Git Gutter](https://github.com/jisaacks/GitGutter)

# Understanding the GIT Model

## Distributed vs Centralized

**Centralized**. One repo and lots of clients.

**Distributed**. One repo with lots of client repos, each with a user.

### Snapshots vs Deltas

In some VCS like SVN, it is the delta/changes in files that are recorded over time. When recording a delta - it is only the changes in each file that gets recorded.

With Git, a snapshot is taken - a full version of the files in the staging area is saved when a commit is done.

### Deltas

![inline](http://git-scm.com/book/en/v2/book/01-introduction/images/deltas.png)

![inline](http://git-scm.com/book/en/v2/book/01-introduction/images/snapshots.png)


## The three states of Git

![inline](http://marklodato.github.io/visual-git-guide/basic-usage.svg.png)
([Source: Visual Git Guide](http://marklodato.github.io/visual-git-guide/index-en.html))

Git has three states, and understanding how git interacts with these states can help make it easier to reason about working with it. The three states in Git are:

### History

History is located in the .git directory, and is where the metadata and
object database of your project is stored. This is what's copied when
you clone a repository

### Working Directory

A version of the project that is checked out and placed on disk.

Its files are pulled out of the compressed database in the .git
directory.


### Staging

A file, in the .git directory, that stores information about what will
go into your next commit.


## How commands interact with git states

Git commands operate over the three states of git - moving changes from working, to staging, to history and back.

* `git add someFile.md` - moves the current saved changes from the working directory, to staging. If you make further edits to someFile.md and save it, those new edits will not be added to your next commit unless you stage those changes.

* `git commit` - moves the currently staged changes, into the history 

* `git checkout <branch>` - moves history into the working directory and switch branches

# Always work on your private feature branch.

In most cases when working on a story, you should be able to work on a private branch on your own fork. 

You should be making changes and commiting to your own branch, and not into master. Changes to be incorperated into the application should be submitted as PR's for review. 

## Work on your own fork.

* Easiest way to fork is from the GitHub UI, simply click on fork
* Once forked, clone and setup the upstream
  * `git clone https://github.com/your-name/git-training.git`
  * `git add upstream https://github.com/rangle/git-training.git`

With this setup, the 'origin' is your own version of the repository, and upstream is the one that you have forked from. 

## Give your branches sensible names.

Branches should be descriptive of the change, and should be named to reflect if it is a fix, feature or chore. 

* `git checkout -b feat-users-change-user-modal`
* `git checkout -b fix-users-correct-email-validation`
* `git checkout -b chore-add-users-to-karma-test-file`

If you are using git-extras, there is a helper command called 'git create-branch' that will set the upstream for you. If you do not do this, you will need to tell git where the branch should go:

`git push --set-upstream origin feat-users-change-user-modal`

# Commit often.

Make frequent commits in the course of doing your work. This makes it easy to go back. It’s ok to commit half-done work, since you will squash those commits later. But do squash (or amend) those commits before submitting a pull request (more on this below).

You can 'perfect' your commits before submitting or merging PR to clean them up. 

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

## Squash commits before submitting a PR

You do not need to always squash a PR down to a single commit, but you should try to cut down on the 'noisy' commits that show
your work in progress/unfinished work. 

You should aim to have commits be 'cherry-pickable', in that if a fix is one branch - and we need that fix in another branch, we shoud be able to pick that commit and apply it else-where without needing to include other commits.

If you need to have several commits within one PR, it could be a sign that the story is too large, and/or that the PR should have been split up across multipul PRs.

Assuming that your master branch of your fork is up to date, to do an interactive rebase:

* git checkout feat-my-branch
* git rebase master -i 

# Stage selectively.

It is tempting to simply do `git add .` to pull all of your changes into the staging area, but this can make it difficult to get smaller commits and have confidence with what you are actually staging.

Tools like gitx can make it easier to review the 'hunks' of a file, and be able to commit portions of a change to file(s) in one commit. 

![inline](http://gitx.frim.nl/images/GitX-Commit.png)

# Do not commit things that should be kept confidential.

When you commit a file, its content becomes part of the project's history and will be visible to any person who will have access to the repository later. For this reason, do not commit credentials, personal information, and other things that ought to be kept confidential.

* Credentials, Passwords, etc should not be kept in the repo.
* If needed for the application, Circle CI, etc - pull them out into environment variables, and set the variables in the needed applications. 
* What is private today, could become public tomorrow - just because a repo is currently private, doesn't mean that it might not become public and have it's history exposed.

# Avoid committing generated artifacts.

* Artifacts that can be automatically generated from your code should generally be kept out of the repository.
* Add these to your .gitignore to avoid unnessicary deltas/diffs
* This include artifacts from the build process
* node_modules, bower_components, etc should be part of your .gitignore file
* Generally speaking - avoid keeping 3rd party code in your repository. The primary exception is if something is not available on bower or npm.

# Update and rebase often.

Your branches and PR's should be small and short-lived, but it is still a good idea to keep them in sync with what is in master. The more often that you resync with the master branch, the less likely you will run into merge issues down the road.

You should rebase off of master frequently, but always at least before submitting a pr, and before merging a PR if you need to squash commits, or if there has been a signifigant delay between sign off and merging. 

Your 'git push' should only be going to your repository, not to the upstream master. 

To rebase a branch off of master:

* `git pull --rebase upstream master`

If you want to do an interactive rebase so you can also squash commits

* `git checkout master`
* `git pull --rebase upstream master`
* `git checkout feat-my-branch`
* `git rebase master -i`

# Use pull requests to integrate into upstream branch.

* Can use the github web-ui to create pull requests
* Have someone review and sign off on your PR with a :+1: or a :shipit:
* If possible - avoid merging your own PRs

# Do not rewrite public history.

History is considered public once another developer is basing their work off of it. If another developer is doing work based off your branch/repo, then it is considered 'public', and commands that rewrite history like:

* `git rebase`
* `git commit --amend`
* `git reset`

should be avoided. This can make it difficult to intergrate changes again after this.

If you are submitting a PR for review that you do not want merged yet, and no one else is going to be working off of your branch - you can still do a squash/rebase before getting it merged into master to clean up your history.

# Learn how to undo

Commit early, commit often, commit incomplete work - why? because Git can make it easy to recover from changes, and when you
can easily pinpoint a single commit to revert a change instead of needing to revert an entire feature - it makes :shipit: happy.

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

### Quick undo


A useful way to use checkout is the command 'git checkout -- .', this
will revert all of your modified files to the latest commit in your
branch. This is useful if you had made a bunch of changes that you no
longer want, and don't want comitted.


### Undoing a single file

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

* create branch, reset-example
* in index/server.js  - add a function, commit, x2
* `git reset head~2` - unstaged, not committed - but still in working
* `git reset head~2 -- hard` - changes get totally removed
