+++
title = "Git"

date = 2019-09-30T00:00:00
# lastmod = 2018-09-09T00:00:00

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

math = false
weight = 100
diagram = true
#markup = "mmark"

edit_page = {repo_url = "https://github.com/Bertbk/tutorial_hugo", repo_branch = "master", submodule_dir="content/tutorial/website/"}
editable = true

[git]
  icon = "github"
  repo = "https://github.com/Bertbk/tutorial_hugo"
  submodule_dir = "content/tutorial/website/"

# Add menu entry to sidebar.
[menu.website]
  name = "Git"
  parent = "II. Continuous Delivery"
  identifier = "git"
  weight = 100
  url=""

+++

Your website looks good on your computer? Good, now you want to deploy it (= get it available online)! But first, you need to copy your code to your git server (here: Gitlab). 


`git` is a powerful software with numerous commands and options but, I can safely assume you are the only *developper* of your website, so you just have to know 5 `git` commands. There are [numerous tutorials for Git](https://git-scm.com/doc) and [cheat sheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf). Here we just see the basic command that you should / will have to use.

## Basic commands

|Command| Short description|
|---|---|
|`git clone source destination` | Copy a whole repository `source` into `destination`. This is done once.|
|`git add file`| 2 usages: first, specifies `git` to track `file`. Second, add that `file` to the next commit.|
|`git commit -m "message of the commit"`| Do a commit, that is like a screenshot or a save, of every added files.|
|`git push`|Send repository (and last commits) **from** the computer **to** the remote server (Gitlab). See [next section]({{<relref "start-deployment.md">}}) before using it!|
|`git pull`| Receive the repository (and missing commits) **from** the remote server (Gitlab) to the computer. You might use this command if you work on different computer and/or multiple developpers on same project (kind of synchronisation)|

## More "advanced" (but not so much)

The following commands are also useful but not in your "every day life":

|Command| Short description|
|---|---|
|`git init`| Initialize a `git` repository. This must be used if the folder do not comes from a `git clone` for example.|
|`git status`| Display the status of the repository: files that has been changed but not commited, files ready to be commited, ...|
|`git log`| Display the history of the last commits.|
|`git checkout file`| Cancel the modification of the `file` and reset it to the last commit. Useful if you are unhappy with your changes and want to come back|
|`git remote -v`| Display the remote server of your git repository.|

## Reset to commit
{{% alert warning %}}
**Huge warning:** you will **lose everything that has not be committed**! This command is **destructive**!
{{% /alert %}}
If you completely messed up your working directory and [want to come back to the last commit](https://stackoverflow.com/questions/4114095/how-do-i-revert-a-git-repository-to-a-previous-commit):
```bash
git reset --hard HEAD
```
or if it's not working:

1. First get the SHA of the last commit (identifier) (copy/past on shell is possible using `shift` + `ctrl` + `c`)

    ```bash
    git log
    > commit 69c453f2d0314af860ee790809ed98861d27ff9b (HEAD -> master)
    ```
2. Revert (either the full SHA or the first 6 characters)
```bash
git reset --hard 69c453
```

## `.gitignore``

You may already have a `.gitignore` file at the root of your folder. This file tells `git` which file it should not tracked. This is very useful as many file should not be tracked and stored by `git`. You probably do not have to modify it, though.

## (Very) short example

{{% alert note %}}
The `git commit` command has an option `-a` that forces to commit **every changes** of **every tracked** file:
```bash
git commit -m "message of commit" -a
```
This is quite usefull as, by doing so, you do not need to `git add` every files you want to commit (`-a` stands for `-all`).
{{% /alert %}}

Let says that I changed the `content/home/about.md` file. Doing
```bash
git status
> Changes not staged for commit:
> 	modified:   content/home/about.md (modified content)
```
I know add the changes to the next commit and commit the changes
```bash
git add content/home/about.md
git commit -m "Update the about page"
```
