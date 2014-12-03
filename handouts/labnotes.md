- have git training branch
- have branch 'empty files' -- skeleton of app
- have branch 'full files' -- final version

git checkout -b components
# make new branch called components
git checkout full-files client/app/components/*
# we have now moved the files from the full-files into the current working branch
git status
# can see that the files are now considered modified
git commit -a -m 'Create repo list component'
git status
git log
# working directory is now clean
git checkout full-files client/app/core/git-api/*
# do a commit without -m and enter in a commit message in a text editor
# pull over git service
git checkout full-files client/app/core/*
git commit -a -m 'Create git service'
# and now the rest
