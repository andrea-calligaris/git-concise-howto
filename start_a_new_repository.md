<p align="center"><a href="index.md">INDEX</a></p>

# Start a new repository

First of all manually create a _GitHub_ repository from the site itself and leave it empty (don't add a _readme_, etc.).

Navigate to the main folder of your project:

`cd my_project`

Make it a _Git_ directory:

`git init .`

The directory _".git"_ will be created inside your project's main folder.

That's the "proof" that it's a git repository. You should otherwise ignore that directory because any change to it will be done via _Git_ commands; the only safe things that you could do to it as a _Git_ beginner are:
* Completely remove it when you want your project folder to not be a _Git_ repository anymore (after ensuring that the content of the project folder is in a state you're ok with, because you can't go back).
* Remove the entire project/repository folder, therefore including its _.git_ child folder; this of course won't change anything online.

Stage files for the initial commit:

`git add readme.md src contrib ...`

Also see [Commit](commit_and_push.md#commit) for useful commands for this phase.

Create a _.gitignore_ file to exclude untracked files, in the repository itself, with a content like:

```
bar.foo
*.bak
```

The _.git_ folder is of course excluded by default.

Stage _.gitignore_ too:

`git add .gitignore`

Take a snapshot of the staging area:

`git commit -m "Initial commit"`

Provide the path for the empty repository you created on _GitHub_:

`git remote add origin https://github.com/yourself/rep_name.git`

Push changes to GitHub:

`git push --set-upstream origin main`

If it says `error: src refspec main does not match any`, you forgot to [change _master_ to _main_](git_configuration_file.md#default-branch-name).

For now just rename it:

`git branch -m master main`

Now your project has version control. You can continue the development and [commit & push](commit_and_push.md) your changes.

<p align="center"><a href="index.md">INDEX</a></p>
