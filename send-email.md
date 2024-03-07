<p align="center"><a href="readme.md">INDEX</a></p>

# Using 'send-email'

## Install

`sudo apt install git-email` or what have you.

## Setup

`git config --global sendemail.from "YOUR NAME <your@email.org>"`

`git config --global sendemail.smtpserver out.email.org`

`git config --global sendemail.smtpuser your@email.org`

If you have different accounts for different projects, you can do the same as above but like:

`git config --global sendemail.PROJECT_NAME.to "project@project.org"`

`git config --global sendemail.PROJECT_NAME.from "YOUR NAME <your@email.org>"`

etc.

Prevent _Git_ from adding yourself to the _Cc:_ field:

`git config --global sendemail.suppresscc self`

This is useful if you are sending the patch to a mailing list and are therefore going to receive a copy of the email anyway.

## Send the patch

Clone the repo, edit and commit normally. Then, instead of pushing, send the patch via email:

`git send-email --dry-run --to project@project.org -1`

(`-1` is "all the changes up to the last commit")

Once the email is sent, there's no going back, so using `--dry-run` is recommended. Check that everything is correct, especially that no unwanted _Cc:_ are being added by _Git_. If everything looks fine, run the command again without `--dry-run` to actually send the mail.

<p align="center"><a href="readme.md">INDEX</a></p>

