<p align="center"><a href="index.md">INDEX</a></p>

# More commands and info


## Named refs (ways to reference commits)

* HEAD: where you are; unless you manually move it, which is rather advanced, it's basically the last commit.
* FETCH_HEAD: the branch which you fetched from a remote repository with your last `git fetch` invocation.
* ORIG_HEAD: the branch you’re merging into.
* MERGE_HEAD: the branch you’re merging from.
* CHERRY_PICK_HEAD: the commit which you are cherry-picking.

## See all branches, including remote ones

`git branch -a`

## See what's going on in this branch

`git status`

## Check the history:

`git log`

Check the history from _main_ to _HEAD_

`git log main..HEAD`

## Advanced stuff

### Detach the HEAD and traverse history

`git checkout main^^` go back two commits

`git checkout main^^^^` go back four commits

Erase history and restart from this commit:

(only use this while doing tests in a private repository)

_git push -f origin HEAD:main_

Call the garbage collector in order to remove old logs:

`git gc`

Enjoy the now clean history:

`git log`

<p align="center"><a href="index.md">INDEX</a></p>
