<p align="center"><a href="index.md">INDEX</a></p>

# Git configuration file

## Default branch name
Change the default branch name from _master_ to _main_ to adhere to the new naming convention:

`git config --global init.defaultBranch main`

Only works from _Git 2.28_.

## Default push behavior

`git config --global push.default <value>`

Leave it at the default (and safest) value:
* _simple_: push the current branch to its upstream branch if it has the same name.

<p align="center"><a href="index.md">INDEX</a></p>

