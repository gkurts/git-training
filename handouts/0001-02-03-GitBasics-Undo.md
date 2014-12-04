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


todo: expand on when git reset vs git revert, revert - undoing 'public' changes, reset = 'local'?
>>>incorperate?
https://www.atlassian.com/git/tutorials/undoing-changes/git-reset
Whereas reverting is designed to safely undo a public commit, git reset is designed to undo local changes. Because of their distinct goals, the two commands are implemented differently: resetting completely removes a changeset, whereas reverting maintains the original changeset and uses a new commit to apply the undo.
<<<

reset example:
- create branch, reset-example
- in index/server.js  - add a function, commit, x2
- git reset head~2 --- unstaged, not committed - but still in working
- git reset head~2 -- hard --- changes get totally removed
