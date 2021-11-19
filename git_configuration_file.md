<p align="center"><a href="readme.md">INDEX</a></p>

# Git configuration file

## Default branch name

Change the default branch name for new repositories, for example to match it with the one that you've set on _GitHub_'s:

`git config --global init.defaultBranch default_name`

Only works from _Git 2.28_.

## Default push behavior

`git config --global push.default <value>`

Leave it at the default (and safest) value:
* _simple_: push the current branch to its upstream branch if it has the same name.

<p align="center"><a href="readme.md">INDEX</a></p>

