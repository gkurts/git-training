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


`git clone`
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

`git remote`
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

TODO: expand on forking / git remote -v,g git remote add

`git fetch`
-----------

Usage:
```
git fetch <remote>
git fetch <remote> <branch>
```

Fetch all of the branches from the repository. This also downloads all of the required commits and files from the other repository.

`git pull`
----

Usage:

```
git pull <remote>
```

Git pull will fetch the remote repository, and merge it. It  bundles git fetch and git merge into a single command.

You can also do a rebase instead of a merge with the usage:

```
git pull --rebase <remote>
```


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
* rebase from master
* push again

Git would reject this change unless you specify the --force flag. It is important however to only do a force push on changes that other developers are not relying on yet.



`git branch`
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
