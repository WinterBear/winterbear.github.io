# Tutorial 1: Version Control

Programming is complicated. Managing large amounts of source code can cause all kinds of problems, expecially when collaborating with multiple developers. The solution to this is version control. Many Version Control applications exist, but none are so widely used as Git.

![git bash](https://i.imgur.com/E6VrvIG.png)

## Installing Git
Installing Git is pretty straightforward, the installer can be found [here](https://git-scm.com/downloads)

The first thing you should do when you have installed Git is to set your user name and email address. This is important because every Git commit uses this information, and changing old commits later is not a simple task. Open the git bash window and use the following commands to configure these:

`git config --global user.name "John Doe"`

`git config --global user.email johndoe@example.com`

You need to do this only once if you pass the --global option, because then Git will always use that information for anything you do on that system. If you want to override this with a different name or email address for specific projects, you can run the command without the --global option when you’re in that project.

You will also want to choose a text editor for git to use as the default. Notepad++ can be configured as follows:

`git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -nosession"`

**The launch arguments -multiInst and -nosession are used to force git's instance of notepad++ to launch as a seperate instance of notepad++ to your usual instance, and to create a seperate session for git usage**

## GUI Alternatives

Git comes with an inbuilt GUI editor, but its features are fairly limited. The git process can be simplified by installing an editor of your choice, I recommend either [SourceTree](https://www.sourcetreeapp.com/) or [GitKraken](https://www.gitkraken.com/), but you should browse the web to find one that fits your needs.

## Creating and Managing a Repository

Repositories can be cloned to your machine from an existing location, or created from scratch.

Creating a new git repository is simple. Once you have installed git, you will be able to navigate to any folder and use the right click menu to open a git bash window within the current folder. All you then need to do is run the command `git init`.

This will initialise a new repo within the current folder. The configuration for the repository is stored within a folder named ".git". You may need to go here if you break your repository.

## Branch Management

Once you've set up your repository you will need to decide what kind of branch structure you will want to use. This is very important to decide early as changing it later is tricky.

For simple, single-user repositories, you may just want to have a master branch and a development branch. You make your commits to the development branch and whenever you want to release a new version of your software you merge your changes from the development branch to the master branch. This is useful as it allows you to create hotfix branches off of master if you need to quickly add a patch to the latest release version without having to merge your development branch.

![git1](https://nvie.com/img/main-branches@2x.png)

This branch structure is simple, but is not optimised for a multi-developer project. For that, we require feature branches.

![git2](https://nvie.com/img/fb@2x.png)

For feature branching to work, each piece of work done against the codebase should be considered a "feature". When you want to add a new feature to your project (whether that is fixing a bug, implementing new functionality or just simple maintenance tasks), you create a new branch off of the development branch. This will give you an exact copy of the codebase at the time of branching for you to work with independently of the rest of the codebase. You then make your commits on your own branch at will until you have completed the feature.

Once you have completed the feature, you will want to merge your feature branch back to the development branch to share your changes with other developers. This can be a very simple process if noone else has committed anything to the development branch since you branched off, as nothing will have changed, but with most multi-developer projects this will often not be the case. If someone has modified the codebase but has not changed any of the same files as you, there will be no merge conflicts and you are free to merge your branch back into the development branch. Occasionally someone will have modified the same files as you, and you will have to resolve the conflicts through a process known as Rebasing which we will cover later.

### Command Reference

|Command|Example|Notes|
|---|---|---|
|`git checkout <branchname>`|`git checkout -b myNewBranchName`|Switches to a branch. Use the -b flag to create the branch first if it does not exist|

### Rebasing

When you make a branch in git, it will have a base point where the branch split from an original branch. A rebase is the process of moving the initial point where the branch split to a point further along the upstream branch:

![git3](https://camo.githubusercontent.com/a65be4a03b4b551df2606fb43c394054ed58d514/687474703a2f2f692e696d6775722e636f6d2f3568725431534f2e676966)

This essentially takes the latest version of the branch you are rebasing on, and tries to reapply all the commits from your branch on top of it. If it finds any conflicts with existing changes on the upstream branch it will pause the process and wait for you to resolve the conflicts. Once you have done so it will continue applying commits until the branch has been fully rebased.

### Pull Requests

## Cherrypicking & Stashing

## Troubleshooting
