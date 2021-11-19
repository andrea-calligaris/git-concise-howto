<p align="center"><a href="readme.md">INDEX</a></p>

# Clone a repository

May be a project on which you are a _collaborator_, o a _fork_ you just made of some project you want to contribute to with _pull requests_.

## Make a fork to contribute to a project you're not an owner/collaborator of

Open [GitHub](https://github.com) and go to a project page; on the top-right click the "Fork" button.

Now you can [clone the fork](#clone-the-repository) on your PC (get the files).

Your repository will now have a remote named _origin_ that points to your fork on _GitHub_. Don’t let the name _origin_ confuse you: this does not point to the original repository you forked from. To keep track of **that** repository add another remote named _upstream_:

`git remote add upstream https://github.com/owner/original_repo.git`

## Clone the repository

Navigate to the folder which will then contain the repository folder:

`cd /mnt/my_repos/`

In the project page on _GitHub_, click on the green button "Code" and copy the HTTPS URL.
Use that to download the repository to your machine:

`git clone https://github.com/owner/repo.git`

Change into the "repo" directory:

`cd repo`

Now you can [Commit & push](commit_and_push.md) your work.

<p align="center"><a href="readme.md">INDEX</a></p>

