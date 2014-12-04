# Fork and Branch

# Github Work Flow
![inline](http://lucamezzalira.files.wordpress.com/2014/03/screen-shot-2014-03-08-at-23-07-361.png?w=650&h=230)

A continuous deployment environment where everything in the `master` branch is deployable.

---

# Fork

A common workflow, especially for open source projects is the 'fork and branch' workflow. This can also be useful for private projects of which you want to have greater access control.

With git, anyone that is a collaborator on a project can have access to create branches, merge, etc on a repository. If you want  control over who can merge into your master or release branches, a way to accomplish this is with Forking.

When creating a fork, a user gets a new copy of the repository that they have full access to.

Examples:
- fork koast-admin-app - https://github.com/rangle/koast-admin-app
- I now have it available at - https://github.com/e-schultz/koast-admin-app
- clone: https://github.com/e-schultz/koast-admin-app.git
- git remote -v --- see origin

Keeping in synch:
- git remote add upstream https://github.com/rangle/koast-admin-app
- git fetch upstream
- git pull upstream
- git pull upstream --rebase

With this workflow, you can allow for a limited set of contributers for the main repo, but people have freedom over their own forks.

When it's time for them to share - issue a pull request, and merge.

## Branching Off

usage:

```
git branch <name of branch>
git checkout <name of branch>
```

To to create a branch and check it out in the same command:

```
git checkout -b <name of branch>
```

Create a new branch off of `master`, commit to that branch locally and push to the server frequently.


## Rebasing

Usage:

`git rebase <name of branch to rebase off>`

As you work and even as you finish, integrate your changes with `master` regularly.

Rebasing changes the base of your branch to the last commit found on another branch, `master` in this case, and replays your changes on top. In essence, the history is rewritten to make it appear that your work was always done after the latest master.

---

## Before a rebase

![inline](http://git-scm.com/figures/18333fig0327-tn.png)

---

## After a rebase

![inline](http://git-scm.com/figures/18333fig0328-tn.png)

---

When you have created a branch, it is a good idea to keep in sync with the master branch. By rebasing frequently, you can help minimize conflicts, and makes it easier for your changes to be integrated into master when you are ready to prepare a pull request.

## Squashing your commits

`git rebase -i <name of branch to rebase off>`

Pick the first commit on your feature branch and squash all subsequent ones on top of it.

This process combines them all into one commit.

## Merging

`git merge --no-ff <name of branch to merge>`

Once the changes have passed the review process, they are merged to the `master` branch.

---

## Merging (continued)

### Before

```
A---B---C topic
/
D---E---F---G master
```

### After
```
A---B---C topic
/         \
D---E---F---G---H master
```
---

## Cherry Pick

`git cherry-pick <sha-1>`

Copy a commit from one branch and apply it to another.


## Pull requests

When a branch is ready to be merged, a pull request is made to start the review process.

---

## Review and discuss

Collaborators and stakeholders can review the commit together and any correction is made to the branch and pushed to update the pull request.
