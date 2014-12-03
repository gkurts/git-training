# Git configuration

## `git config --global user`

`.name <name>`: Setup your name.
`.email <email>`: Setup your email.

Set the name and email that will be attached to your commits.

---

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
