## Good Commits

![original](http://imgs.xkcd.com/comics/git_commit.png)
---

Do's
----
- keep commit changes as small as possible
- describe what was changed and why
- limit first line to 50 characters
- insert a blank line after first line
- wrap subsequent lines at 72 characters

Don'ts
------
- mix whitespace with functional code changes
- mix unrelated functional code changes
- send large feature in a single commit

Model Git commit message
------------------------

```
Capitalized, short (50 chars or less) summary

More detailed explanatory text, if necessary.  Wrap it to about 72
characters or so.  In some contexts, the first line is treated as the
subject of an email and the rest of the text as the body.  The blank
line separating the summary from the body is critical (unless you omit
the body entirely); tools like rebase can get confused if you run the
two together.

Write your commit message in the imperative: "Fix bug" and not "Fixed bug"
or "Fixes bug."  This convention matches up with commit messages generated
by commands like git merge and git revert.

Further paragraphs come after blank lines.

- Bullet points are okay, too

- Typically a hyphen or asterisk is used for the bullet, preceded by a
  single space, with blank lines in between, but conventions vary here

- Use a hanging indent
```

## `git commit --amend`

Add any staged changes to the last commit and amend the commit message (optional).

Useful for when you commit early and forget to add some files or when you make a mistake in the commit message.

## `git stash`

Save the uncommitted changes in the working directory and the staging area and go back to a clean working directory.
