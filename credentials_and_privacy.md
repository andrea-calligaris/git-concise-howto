<p align="center"><a href="readme.md">INDEX</a></p>

# Credentials and privacy

## Email privacy
The best thing that you can do for email privacy / spam control is to have a different real email address to use with _GitHub_ and related services, preferably with email forwarding to your other email address(es), and use this email address to sign up to _GitHub_ and to push commits with _Git_.

The alternative is to hide the email address on both _GitHub_ and _Git_:

on _GitHub_'s email settings, check:

* _Keep my email addresses private_, to make _GitHub_ generate a _no-reply_ email address for you.
* _Block command line pushes that expose my email_, to prevent mistakes while using _Git_.

Now, when [you tell _Git_ your identity](#tell-git-who-you-are), use that _no-reply_ email address.

## Tell Git who you are

(this is different than [making git remember your credentials](#make-git-remember-your-credentials))

`git config --global user.name "your name"`

`git config --global user.email "your email"`

or

`git config --global user.email "the no-reply email"`

depending on what you choose for your [email privacy](#email-privacy).

The _--global_ option is so it's for all repositories.

## Password

Only use [tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) in place of passwords (it's mandatory anyway) so in case of data theft you just need to delete the tokens.

## Make Git remember your credentials

`git config --global credential.helper store`

They will be saved in _~/.git-credentials_.

To reset the credentials just delete such file.

<p align="center"><a href="readme.md">INDEX</a></p>

