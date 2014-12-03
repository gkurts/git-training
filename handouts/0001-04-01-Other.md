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
