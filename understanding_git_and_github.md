<p align="center"><a href="readme.md">INDEX</a></p>

# Understanding Git and GitHub

## Ultra terse basics
_Git_ helps you to keep track of changes in the code of a project and to develop together with people.
_GitHub_ is a site where you can host _Git_ _repositories_ (projects).

You _clone_ a _repository_ from _GitHub_ to your machine, you make a _local branch_, you fix a bug, you _commit_ that change, you _push_ your change online, and finally you open a _pull request_ so the owner can inspect it and decide to _merge_ it or not with its original _repository_.

## Some definitions
* `VCS`: version control system, which _Git_ is.
* `repository`: a project, basically; where the project is stored: could be _GitHub_ and/or your PC.
* `remote`: the generic word for a repository hosted online, generally at _GitHub_. Also the _reference_ to it.
* `fork`: your personal online copy of a repository of someone else.
* `commit` / `snapshot`: the "revision", as called in other VCSs; a given state of the project; also as a verb: `to commit`: to create a snapshot.
* `branch`: a simple pointer (or reference) to the head of a line of work.
* `tag`: just another pointer, used e.g. to say that from this tagged commit starts the _v2.1_ of the project.
* Naming conventions for repositories and branches:
  * `master` (`main` on _GitHub_...): the primary branch of the repository.
  * `origin`: your fork (or your own original repository).
  * `upstream`: the repository you forked from.
* `merging`: putting a forked history back together again; the result is a `merge commit`.
* `merge conflict`: when trying to merge, two commits changed the same file; needs to be solved before successfully concluding a merge.
* `reference` / `ref`: basically a "pointer" to a commit; in practice it's a _SHA-1_ value of the commit.
* `HEAD`: a symbolic reference to the branch you're currently on.
* `branch_name`: a **local** branch.
* `origin/branch_name`: a **remote** branch.
* `tracking` / `setting the upstream to`: a `tracking branch` has a direct correlation to a remote branch, so if you do e.g. `git push`, _Git_ automatically knows which server and branch to push to.
After cloning a repository, it generally automatically creates a _master_ branch that tracks _origin/master_; however you can switch to and create other branches.
* `fast-forwarding`: what happens when you update your local repository with `git pull` and you get no issues; technically it's merging two or more commits in one go, when there is no divergent work to merge together (and therefore no `merge conflicts`). In yet other words, to _fast-forward_ means to advance your local _HEAD_ until it matches the last commit (or a given specified commit) of _origin_.

## Understand visually

(adapted from https://git-scm.com/docs/git-checkout)

```
           HEAD (refers to branch 'master')
            |
            v
a---b---c (master)
    ^
    |
  tag 'v2.0'

```

Commits: `a`, `b`, and `c`

`master`: a branch which refers to commit `c`

`HEAD`: a symbolic reference to the branch you're currently on

`tag 'v2.0'`: a tag which refers to commit `b`

Now we change some code; then, we commit it:

`git add...; git commit...`:

```
               HEAD
                |
                v
a---b---c---d (master)
    ^
    |
  tag 'v2.0'

```

We've created commmit `d`.

`master` has been updated, and so has `HEAD`, which always points to `master`.

Now, if we want, we can `git push` such commit online.

<p align="center"><a href="readme.md">INDEX</a></p>
