<p align="center"><a href="readme.md">INDEX</a></p>

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

Check the history from _master_ to _HEAD_

`git log master..HEAD`

## Check the changes you've done in the last commit

Since you cannot use `diff --cached` anymore, you can do:

`git diff HEAD^ HEAD` or `git show`

## A branch name has been changed in upstream. Change it locally too:

`git branch -m old_branch new_branch`

`git fetch origin` or `git remote -v update`

`git branch -u origin/new_branch new_branch`

`git remote set-head origin -a`

`git fetch --prune`

## Advanced stuff

### Detach the HEAD and traverse history

`git checkout master^^` go back two commits

`git checkout master^^^^` go back four commits

### Erase recent history and restart from a given commit:

**(only use this while doing tests in a private repository)**

Move the _HEAD_ as shown above. Then push:

`git push -f origin HEAD:master`

Call the garbage collector in order to remove old logs:

`git gc`

Enjoy the now clean history:

`git log`

### Delete the commit history and force push with a fake date

**(only use this while doing tests in a private repository)**

Create an orphan branch (without a commit history):

`git checkout --orphan temp_branch`

If you do e.g. `git branch -a` you won't see it, it's normal.

Add all files:

`git add -A`

Commit the changes with a fake date (*GIT\_AUTHOR\_DATE* only):

`git commit --date "2020-01-01T16:00:00 +0100" -m "Initial commit"`

Change *GIT\_COMMITTER\_DATE* too:

`git filter-branch --env-filter 'export GIT_COMMITTER_DATE="$GIT_AUTHOR_DATE"'`

Delete the master branch:

`git branch -D master`

Rename the temporary branch to master

`git branch -m master`

Force update to repository

`git push --force origin master`

Delete the local repository folder.

Download the repository from scratch, to get rid of logs, old objects, etc.:

`git clone https://github.com/owner/repo.git`

<p align="center"><a href="readme.md">INDEX</a></p>

