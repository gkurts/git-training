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

With this workflow, you can allow for a limited set of contributers/maintaieners for the main repo, but people can do whatever they want on their own repositories.

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
