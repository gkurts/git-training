# Introduction

## What this session will cover

The agenda will be:

- What is git
  - Distributed vs Central source control
  - Snapshots of changes vs Deltas
  - Three states of git: History, Staging, Working
- Git Command Basics
  - Saving changes (init, status, add, commit)
  - Viewing history (log)
  - Undoing (reset, revert, checkout)
  - Collaboration (clone, push, pull, branch)
- Git workflows and best practices
  - commit messages
  - git ignore
  - branch / pull / pull / forks / etc
  - Merge, rebase and resolving conflicts
- Some advanced git concepts
  - git hooks
    - client
    - web
    - server
- Git integrations
  - MagnumCI
  - Heroku

# What is GIT

Git is an open source Distributed Version Control System (DVCS). O

## Distributed vs Centralized

**Centralized**. One repo and lots of clients.

**Distributed**. One repo with lots of client repos, each with a user.

## Snapshots vs Deltas

In some VCS like SVN, it is the delta/changes in files that are recorded over time. When recording a delta - it is only the changes in each file that gets recorded.

With Git, a snapshot is taken - a full version of the files in the staging area is saved when a commit is done.

### Deltas

![inline](http://git-scm.com/book/en/v2/book/01-introduction/images/deltas.png)

![inline](http://git-scm.com/book/en/v2/book/01-introduction/images/snapshots.png)

## Lightweight Branches

## Easily Curated Commits

Since Git stores full versions of the files with each commit, and everything is stored locally - it's easier to curate commits (expand this)

# Git configuration

## `git config --global user`

`.name <name>`: Setup your name.
`.email <email>`: Setup your email.

Set the name and email that will be attached to your commits.

## `git config --global alias`

Set short forms for frequently used commands.

Examples:

```
git config --global alias.st status
git config --global alias.ci commit
git config --global alias.br branch
git config --global alias.co checkout
git config --global alias.df diff
git config --global alias.lg 'log -p'
git config --global alias.lg1 'log --graph --abbrev-commit --decorate --date=relative --format=format:\'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)\' --all'
```

# The three states of Git

![inline](http://marklodato.github.io/visual-git-guide/basic-usage.svg.png)

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
