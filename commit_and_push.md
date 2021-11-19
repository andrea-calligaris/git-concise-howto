<p align="center"><a href="readme.md">INDEX</a></p>

# Commit & push

Please first see [Understanding Git and GitHub](understanding_git_and_github.md) (it's really short!) so while following this document you'll better understand what you're doing.

## Typical commit & push procedure

* [Create a new branch](#create-a-new-branch) or [track an existing branch as a owner/collaborator](#track-an-existing-branch-as-a-ownercollaborator)
* [Update the repository](#update-the-repository)
* Make your changes to the files
* [Update the repository](#update-the-repository) again if needed
* [Commit](#commit)
* [Push](#push)
* [Fix the merge conflicts](#fix-merge-conflicts) if needed
* [Make a pull request](#make-a-pull-request)
* [Delete the branch](#delete-the-branch)

## Create a new branch
Either in your fork as a contributor or in the original repository as a collaborator, to make changes to the code, create a new branch where you'll code, commit, and push your changes.

#### Why creating a branch

You could indeed just do your changes on _master_, however creating branches is the proper _Git_ workflow, and it keeps your changes organized and separated from the _master_ branch so you can submit multiple pull requests with ease.

## Case A: Create a new branch in your fork

`git branch my_branch`

Switch to it:

`git checkout my_branch`

You're not specifying here a remote to track (using `--track` or `--set-upstream-to` options), because it's a new branch. You'll later push this new branch online with `git push`.

### Case B: Create a new branch in the original repository as a owner/collaborator

Same as [case A](#case-a-create-a-new-branch-in-your-fork).

## Track an existing branch as a owner/collaborator

Check all the branches, including the remote ones:

`git branch -a`

Switch to the one you want (this will automatically create a tracking local one):

`git checkout new_feature_branch`

## Update the repository

### Updating a fork

Sync it to keep it up-to-date with the upstream repository.

`git fetch upstream`

Check out your fork's local default branch:

`git checkout master`

Then (like `git pull` which is `fetch` + `merge`):

`git merge upstream/master master`

and not `git pull`, because it will pull from `origin`, which is probably already up to date, but it's not the original repository, it's your fork.

If you already wrote some code, instead of merging, you can replay your local work on top of the fetched branch like a `git pull --rebase`, with:

`git rebase upstream/master`

#### If 'git fetch upstream' doesn't work

Your repository probably has a remote named _origin_ that points to your fork on _GitHub_. Don’t let the name _origin_ confuse you: this does not point to the original repository you forked from. To keep track of **that** repository add another remote named _upstream_:

`git remote add upstream https://github.com/owner/original_repo.git`

### Updating an original repository (not a fork)

Bring your remote refs up to date:

`git remote -v update`

If you want, check the new commits in the remote branch:

`git log`

 (`Q` key to quit)

Check if the branch that you are tracking is ahead, behind, or has diverged:

`git status`

If behind, update the branch by fast-forwarding:

`git pull`

## Commit

Check if you are in the correct branch:

`git branch`

Check which files you changed:

`git diff --name-status`

or without _--name-status_ if you want to go through all the changes (`Q` key to quit).

Stage the changed files:

`git add readme.md LICENSE.txt etc.`

or, to stage all changes, simply:

`git add .`

To remove a file:

`git rm <file>`

or, if you've already manually deleted it, stage it:

`git add <file>`

Check if you've staged the correct files:

`git diff --name-status --cached` or `git diff --name-status --staged` (synonyms)

or without _--name-status_ if you want to go through all the changes (`Q` key to quit).

If you happen to make more modifications to the code, you can simply use the various commands above again to stage the new changes.

Take a snapshot of the staging area (anything that's been added):

`git commit -m "Update readme.md"`

or, if you want to write an extended message, just do:

`git commit`

for _Git_ to open the assigned text editor. After the comments (`#`), write the subject (the title) of the commit. Then have a new empty line, and from there you are going to type the body (the description) of the message.

### How to write a good commit message

Which is very important for any project, to then easily inspect the history (logs).

The seven rules:
* Separate the subject from the body with a blank line.
* Limit the subject line to 50 characters.
* Capitalize the subject line.
* Do not end the subject line with a period.
* Use the imperative mood in the subject line ("Fix bug" and not "Fixed bug" or "Fixes bug.").
* Wrap the body at 72 characters.
* Use the body to explain _what_ and _why_ vs. _how_.

## Push

After you've created a commit, you want to actually push it to _GitHub_ with the `git push` command:

### Case A: Push the branch to your forked repository

If you've not specified the upstream yet:

`git push --set-upstream origin my_branch`

If it is specified already:

`git push`

You can now [make a pull request](#make-a-pull-request).

### Case B: Push the branch to the original repository as a owner/collaborator

Same as [Case A](#case-a-push-the-branch-to-your-forked-repository).

### Case C: Push directly on origin/master, as a owner/collaborator
If you are the owner, you can push directly to _master_.

If you've not specified the upstream yet:

`git push --set-upstream origin master`

If it is specified already:

`git push origin master`

or simply:

`git push`

If it is specified already but the name of the branches are different, i.e. you are on _my_branch_ but you want to push on _origin/master_:

`git push origin HEAD:master`

or change the [default.push value](git_configuration_file.md#default-push-behavior) in the configuration file to something different.

## Fix merge conflicts

First of all see what

`git status`

says. It should tell you which files have conflicts.

### Case A: You both changed the content in that/those file(s).

Open the file and you'll see that it contains the typical _Git_ markers intended to show which lines have conflicts, like `<<<<<<<`.
Change the file as it suits you, removing all _Git_ markers.

Then, stage the changes:

`git add <file>`

Commit your changes:

`git commit -m "Resolve merge conflict by incorporating both suggestions"`

and push:

`git push`

### Case B: You edited a file but another person removed it.

`git add <file>` to add it back.

or

`git rm <file>` to remove it.

Commit your changes:

`git commit -m "Resolve merge conflict by deleting <file>"`

and push:

`git push`

## Make a pull request
Go to [GitHub](https://github.com) and navigate to the branch in your forked repository. Here you can create a pull request. The owner and collaborators of the original repository will check it and will then decide if they want to merge or not your contribution.

If they do, you can then [delete your branch](#delete-the-branch).

## Delete the branch

### Delete the branch remotely
You can do it directly on _GitHub_ or you can do:

`git push origin --delete my_branch`

### Delete the branch locally

While you were waiting for the pull request merge, you may have made other commits in this branch; to be sure not to lose code, check:

`git log my_branch ^master --no-merges`

If the only not merged commit is the one of the pull request merge, you're good to go:

Get out of the branch and go to any other one:

`git checkout master`

Force deletion with the _-D_ option:

`git branch -D my_branch`

<p align="center"><a href="readme.md">INDEX</a></p>
