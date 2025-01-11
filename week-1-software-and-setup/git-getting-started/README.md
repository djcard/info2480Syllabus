---
description: >-
  Goal: By the end of this document, you will have a very rough idea of what git
  does.
---

# Git: Getting Started

Github.com is a website designed to help developers share code with each other. This can be people on the same development team who run the risk of overwriting each others changes if multiple people are working on the same files or complete strangers who find some code they can use that someone else has made available.&#x20;

The underlying technology behind sites like Github.com and Gitlab.com is an application called `git`. This was developed by Linus Torvald, the developer of Linux, and has a number of uses. Git allows people to share code but, more importantly, it allows developers to have multiple version of the same code without losing the original and then merge those versions together if the changes work out.

Git is the program behind sites like Github, Gitlab and others, but it it can also be installed on any desktop or laptop like we're going to do here. At the heart of git is the "repository". A git repository works a bit like a library. However, instead of having several different titles, it has several versions of the same title. In this case, your code. Each version is called a **BRANCH**. There is the primary version of your code which is called the "Main" or "Master" branc&#x68;**.** This is usually considered the "production" version of the code and is typically the version of your site which is going to be seen by your target audience.&#x20;

Let's say your main branch is working as is, but then you find a bug or think of a new feature you need to implement. Rather than risk breaking the current version and not having a working website, you make another branch and give it a name, say "change-color-of-navbar". Branches can be for very small changes or much large overhauls.&#x20;

This branch is a complete copy of the site, however, it's not in a new folder or new location on your computer, it is in the exact same folder as your original site. How this is possible is what make git so powerful. Rather than have multiple versions of your site in folders all over the place where it is easy to lose track of which version is what, you **Check Out** a branch from the git repository. When you check out a branch, git will pull the correct version out of the repository and put it in that folder. You can then do the work you want on the branch and when you are done, you check in or **COMMIT** those changes to the repository.&#x20;

You now have two branches in the repository - `main` and `change-color-of-navbar` with all of your changes. Now what? Once you are sure that all your changes are done AND you haven't broken anything from the original site, you can **MERGE** the `change-color-of-navbar` branch into the `main` branch. That takes all of the changes you made and moves them into the main branch. You can now deploy your main branch to your production site knowing that it is in good working order. At this point you can delete the `change-color-of-navbar branch` if you choose since it is no longer needed.

&#x20;If you've never used it before or have never worked in a development team, this might seem like overkill. However, there are many many advantages to this approach that you might not fully appreciate unless you've worked on large projects without a version control system. This approach can keep you more organized and focused on essential tasks. It allows multiple people to work on the same file and git usually does a good job in merging everyone's changes together.&#x20;

If this is confusing, (and it is confusing!) it will make more sense after you do it a few times. Also, just a warning, be prepared to make a few mistakes. It takes practice to get the workflow correct.
