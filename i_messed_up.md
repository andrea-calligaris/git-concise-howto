<p align="center"><a href="index.md">INDEX</a></p>

# I messed up!

## It says there are merge conflicts!

See [Fix merge conflicts](commit_and_push.md#fix-merge-conflicts).

## My pull request has not been accepted and they want me to update the commit without making another one (amend the commit)

See [Change the already pushed commit (amend the commit)](#change-the-already-pushed-commit-amend-the-commit).

## I want to delete the last commit

To keep the work you've done:

`git reset --soft origin`

or

`git reset --soft origin/<branch>`

To destroy the work you've done:

`git reset --hard origin`

or

`git reset --hard origin/<branch>`

### I have already pushed online though!

[Revert a commit by making a new one which goes back to previous code](#revert-a-commit-by-making-a-new-one-which-goes-back-to-previous-code) or [force a push](#force-a-push).

## Force a push

`git push --force-with-lease`

_--force-with-lease_ stops the command if there are other other commits ahead of you. If that happens, you have no other option that to [make a new commit which reverts back to previous code](#revert-a-commit-by-making-a-new-one-which-goes-back-to-previous-code).

The _--force_ option instead is the aggressive one, which overwrites any eventual work on the remote branch. Don't use this in a **public** repository: "rewriting history" is very bad practice; if you do, people who have already cloned your repository would have to be informed of this forced push and they'll have to manually fix their local history e.g. with `git pull --rebase`; instead [make a new commit which reverts back to previous code](#revert-a-commit-by-making-a-new-one-which-goes-back-to-previous-code).

Where you can use _--force_?

* In a **private** testing repository, e.g. to simplify the history (logs).

* On a small **public branch** of a **fork** you made, e.g. for preparing a small bugfix for a pull request.

### I forced a push but it says "Everything up-to-date"!
Possible situation: [you did your changes on the main branch](#i-did-my-changes-on-the-main-branch-on-my-fork-and-now-i-cant-reset)

### I did my changes on the main branch on my fork and now I can't reset
You are not working on a new branch but on the main branch of your fork. In this case you need to get the data back from the upstream:

`git reset --soft upstream/main`

`git push --force-with-lease`

### The push was rejected because of merge conflicts

See [Fix merge conflicts](commit_and_push.md#fix-merge-conflicts).

## Revert a commit by making a new one which goes back to previous code

Revert the last commit:

`git revert HEAD`

In the text editor, change the message if you want and save the file.

Then do a regular push:

`git push`

## Revert multiple commits

Prepare a new commit reverting the last 3 commits:

`git revert -n HEAD~3..HEAD`

`git commit -m "Revert last 3 commits, sorry"`

Regular push:

`git push`

## Amend the commit

### Change the commit message

`git commit --amend`

Then, in the text editor, change the message and save the commit.

### Change the committed files

Make sure you don't have any unwanted changes staged before doing this or they will get committed too.

Change what you need to. E.g. if you forgot to include _my_file.cpp_ or you have to make some changes to it, you have to stage it again:

`git add my_file.cpp`

Amend:

`git commit --amend --no-edit`

_--no-edit_ is to leave the commit message unchanged.

### I have already pushed online though!

Make another commit or [force a push](#force-a-push).

## I want to reset the changes and I have not committed yet

Get back the original code:

`git restore '*.cpp'`

Un-stage files that you staged with `git add`:

`git reset '*.cpp'`

Revert everything:

`git restore :/`

## I changed the code and started staging changes with `git add` but then I realized I'm on the wrong branch

See [I want to reset the changes and I have not committed yet](#i-want-to-reset-the-changes-and-i-have-not-committed-yet).

## `git status` lists files in "Changes not staged for commit", even though I did an hard reset

It could be a problem about permissions. Do:

`git diff`

If the output is something like:

```
diff --git a/src/main.cpp b/src/main.cpp
old mode 100644
new mode 100755
```

this means that the file in your hard disk has a different permission (_mode_) than what's in the repository.

This may happen for example when moving a Git repository across different hard drives / partitions, or when moving it across _Windows_ and _Linux_.

First of all, notice that Git **only tracks whether a file is executable or not**, not the full set of _*nix_ permissions. So for Git to recognize a change, you can only do `+x` or `-x`.

Anyway:

### Fixing the problem: Option A: ignore permissions

You can make Git ignore the executable bit by doing:

`git config core.filemode false`

That will solve the problem; however, if you do want some files to have executable permissions and you want to save this information on the online repository, you don't want to do that; in this case what you need to do to solve the issue is to change the permissions of the files in your hard drive to match the online repository again:

### Fixing the problem: Option B: match permissions to the online repository

Remove the executable bit from all files:

`sudo chmod -R -x .`

This will also revoke your ability to list the directories, so fix it:

`sudo chmod -R +X .`

Now, if you do have any files you want to keep executable, such as _.sh_ scripts, you'll need to revert those. For each of those files do:

`chmod +x ./compile.sh`

### If you're using a shared folder in _VirtualBox_

Do not mount the shared folder automatically, because it will mount it with different and unchangeable permissions. In the machine options, give a name to the folder (in this example `shared_folder_name`), uncheck _Automatic mount_, and do not specify a mount point. Then, edit your _/etc/fstab_:

`shared_folder_name /mnt/existing_folder vboxsf rw,uid=1000,gid=1000,nosuid,nodev,nofail 0 0`

## I can't switch branches, it says: "Commit your changes or stash them before you can merge"

* Option 1: commit the changes.

* Option 2: stash them in the stack (where you push and pop them from):

  `git stash`

  To pull the stash:

  `git stash pop`

* Option 3: discard the changes:

  `git reset --hard`

  or

  `git checkout --track --force origin/branch`

## It says "There is no tracking information for the current branch."

`git branch --set-upstream-to=origin/remote_branch local_branch`

## By typing `git checkout` and pressing TAB, I get a ton of crap

Keep in mind that those all caps names like `HEAD` are meant to be there, see [Named refs](more_commands_and_info.md#named-refs-ways-to-reference-commits).

Clean outdated branches:

`git fetch --prune`

### There are still outdated branches!

Maybe it's a tag:

`git tag --delete <tag_name>`

<p align="center"><a href="index.md">INDEX</a></p>
