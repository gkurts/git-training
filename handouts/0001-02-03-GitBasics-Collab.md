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
- git remote
- git fetch
- git pull
- git push
- git branch

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
repositories. Remotes act as aliases to other repositires to let you
easily work with them by being able to request changes, push changes,
etc by short name.

`git remote` will list the remotes setup for your repository.

`git remote -v`
---------------

`git remote -v` will display a more verbose output of your remotes,
including the url and if you can fetch/push to it.

```
git remote -v
origin  https://github.com/e-schultz/git-training-app.git (fetch)
origin  https://github.com/e-schultz/git-training-app.git (push)
```

TODO: expand on forking / git remote -v,g git remote add

`git fetch`
-----------

Usage:
```
git fetch <remote>
git fetch <remote> <branch>
```

todo: expand

`git pull`
----
todo: expand



`git push`
----
todo: expand
