# Introduction


## What this session will cover

This training session aims to get you up and running with Git quickly, covering some of the core concepts behind git, the most common commands and their uses, some more advanced use cases and if time allows - examples of how easily Git can integrate with third party services to help manage your builds, testing and deployment.

The agenda will be:

- What is git
  - Distributed vs Central source control
  - Snapshots of changes vs Detlas
  - Explaining git states - working, staging and history
- Git Command Basics
  - Saving changes (init, status, add, commit, checkout)
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

In some VCS like SVN, it is the delta/changes in files that are recorded over time. When recording Detlas - it is only the changes in each file that gets recorded.

With Git, a snapshot is taken - a full version of the files in the staging area is saved when a commit is done.

### Deltas

![inline](http://git-scm.com/book/en/v2/book/01-introduction/images/deltas.png)

![inline](http://git-scm.com/book/en/v2/book/01-introduction/images/snapshots.png)

## Lightweight Branches

TODO: expand

## Easily Curated Commits

TODO: expand

Since Git stores full versions of the files with each commit, and everything is stored locally - it's easier to curate commits (expand this)
