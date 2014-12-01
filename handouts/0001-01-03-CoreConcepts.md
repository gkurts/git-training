the three states of Git
-----------------------

Git has three states, and understanding what these states are and how
various git commands interact with these states can help make it easier
to reason about working with it. The three states in Git are:

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

![inline](http://marklodato.github.io/visual-git-guide/basic-usage.svg.png)
