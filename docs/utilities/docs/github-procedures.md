# Common GitHub Procedures

We expect each student to use two GitHub repositories, one for personal assignments and one for team assignments, and for you to use these repositories to collaborate on and store source code and other files over the course of the semester. Please be mindful to submit individual and team assignments in the correct repositories.

## GitHub Cheat Sheet

**[GitHub Cheat Sheet](/docs/utilities/docs/github-git-cheat-sheet.pdf)**

## Cloning a Repository

Cloning is the process by which the content in a Git repository is transferred to your local computer. GitHub provides many ways to do this.

**If you're using the GitHub desktop application**, you can simply click the ``Clone in Desktop`` button found on the front page of every GitHub repository.

This will open the GitHub desktop application and walk you through the process of cloning the repo onto your computer.

**If you're using the command line interface**, you can reference [the Git website](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository) and follow their instructions for ``Cloning an Existing Repository``, using the ``HTTPS clone URL`` found on the front page of every GitHub repository.

#### Command Line Example

If you're trying to clone this repository, the console command is:

    git clone https://github.com/BU-EC444/code-examples.git

## Creating a Branch

There are many ways to create new branches in your Git repository.

When creating a branch, be mindful of the branch you're currently working in. That is, if you want to create a new Feature Branch from ``master``, make sure you have the ``master`` branch checked out before following any of these steps.

See:

[GitHub Desktop Client -- Creating a New Branch](https://help.github.com/en/desktop/contributing-to-projects/creating-a-branch-for-your-work)

[GitHub Website -- Creating a New Branch](https://github.com/blog/1377-create-and-delete-branches)

[Command Line -- Creating a New Branch](https://github.com/Kunena/Kunena-Forum/wiki/Create-a-new-branch-with-git-and-manage-branches)

#### Command Line Example

If you want to create a new branch called ``foo``, the console command is:

    git branch foo

## Committing Changes to a Branch

You need to add and commit changes to a branch before they can be pushed to the server, and before you perform any merge operations on the branch.

See:

[GitHub Desktop Client -- Committing Changes](https://help.github.com/en/desktop/contributing-to-projects/committing-and-reviewing-changes-to-your-project)

[Command Line -- Committing Changes](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)

#### Command Line Example

If you want to commit all current changes to the active branch, the console commands are:

    git add -A
    git commit -m "Describe what this commit is all about"

## Syncing Changes to the Server

"Syncing" a branch is the process of pushing any local changes to the GitHub server, and pulling any changes from the server into your local branch.

In the GitHub desktop application, this is performed by simply hitting the 'sync' button in the top-right of the application.

From the command line, this is accomplished by first committing your changes, then pulling any changes made to the remote server with ``git pull``, then pushing any local changes up to it with ``git push``.

## Merging Changes

When one branch is merged into another, changes made to it are reconciled with the branch it is being merged into.

When merging a downstream branch into an upstream branch (such as a particular feature branch into `master`), the safest way to proceed is to [create a Pull Request](https://help.github.com/en/articles/creating-a-pull-request).

When merging an upstream branch into a downstream branch (such a feature branch into a personal branch), one can use either the GitHub Desktop Client or the command line to manually merge the two.

#### Command Line Example

If you want to merge the branch ``Feature`` into the branch ``Personal``, the console commands are:

    git checkout Feature
    git pull
    git checkout Personal
    git merge Feature
    git push

Sometimes, an attempted merge will result in **merge conflicts**. These happen when two people modify the same files at the same time, and they're expected to happen at some point during every project. There are [guides written on how to resolve merge conflicts](https://css-tricks.com/deal-merge-conflicts-git/), and you're also welcome to ask a TA for help.

### Creating a Pull Request [the better way]

Pull requests are a formal way to ask for changes to be merged (pulled) from one branch and into another. Usually, these requests are structured so that the upstream branch (for example, ``master``) is requested to pull changes from a downstream branch (such as a particular feature branch).

These requests can be initiated in either the GitHub Desktop Client or on the GitHub website.

[GitHub Desktop Client -- Creating Pull Requests](https://help.github.com/en/articles/creating-a-pull-request)

[GitHub Website -- Using Pull Requests](https://help.github.com/articles/using-pull-requests/)

## Discarding Changes
**THIS WILL DESTROY ANY UN-COMMITTED WORK DONE ON A BRANCH, AND SHOULD BE A LAST RESORT.**

When you're **absolutely sure** you want to nuke all un-committed changes, the console command is:

    git reset --hard HEAD

Don't say we didn't warn you!
