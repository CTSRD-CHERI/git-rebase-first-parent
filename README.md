# git rebase-first-parent

This wrapper around `git rebase` supports rebasing merge commits, treating them
as relative to their first parent (as if running `git cherry-pick
--mainline=1`), whilst preserving all other parents. This is intended to
reflect how one normally wishes to rebase a merge from an upstream branch,
including subtree merges for vendor imports.

As an example, suppose you have the following commit graph:

```
A---F---G  upstream
 \
  C---E  local
 /   /
B   D
```

Running `git rebase-first-parent upstream` on `local` (or by passing it as the
`<branch>` argument) will result in the following commit graph:

```
A---F---G  upstream
         \
          C'--E'  local
         /   /
        B   D
```

To use this tool, ensure the three scripts present in this repository all
appear in your `PATH`.

The subset of `git rebase` options supported should behave as their
equivalents.

```
usage: git rebase-first-parent [-i | --interactive] [--onto <newbase>] [<upstream> [<branch>]]

    -h, --help            show the help
    -i, --interactive     let the user edit the list of commits to rebase
    --onto <newbase>      rebase onto given branch instead of upstream
```
