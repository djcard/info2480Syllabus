# Cloning and Forking

**Goal: By the end of this document, you will understand what Cloning and Forking mean when it comes to git.**

Previously, we created a git repository on our local machine, made a branch, made some changes and then checked that branch and those changes back in again. All of that happened on our local machine. [Github.com](http://github.com), makes it easy to find other projects which we would either like to contribute to by adding a feature or fixing bug.

To do that, we usually copy the entire repository down to our local machine so we can work on it. When we make that copy, we now have a `LOCAL` copy and a `REMOTE` copy. The remote copy is still in the original owners account. This is called `CLONING`. When we clone a repo, we create a local repo on our machine, perhaps make a branch to use to make edits and then check those changes back into our local repo. If we choose to, and we have permission, we can then `PUSH` those changes back up to the remote repository. If it is not our account or we don’t have permission, we can create something called a `PULL REQUEST` which allows the account owner to look over your changes and choose to accept them or not.

Conversely, when you copy a repo from one account on Github to another account on Github ( such as your own ) it is called `FORKING`. The intention here is that you will clone the repo you forked onto your local machine and the forked repo will act as your remote repo. All changes you make will be checked into the repo on your account, not the original owners. If down the road, you wish the original owner to consider accepting your changes into their project, you would then create a `PULL REQUEST (PR)` or `MERGE REQUEST (MR)` for that owner to look over your changes and choose to merge them into their project or not.

In this class you will use a repo you create in your own Github.com account and use that to share your work with me.

Key points

* Copying a repository from an account online is called cloning.
* Copying a repository from an online account to another online account is called forking.
* When you want changes you’ve made in one repo to be merged into a repo owned or managed by someone else, you create a pull request or merge request.
