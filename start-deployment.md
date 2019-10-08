+++
title = "Manual Deployment"

date = 2019-09-30T00:00:00
# lastmod = 2018-09-09T00:00:00

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

math = false
weight = 40
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
  name = "Manual Deployment"
  parent = "I. Getting Started"
  identifier = "deployment_rsync"
  weight = 40
  url=""

+++

This page explains how to deploy your website *manually*. I still recommend you to learn `git` to store and save your source code (which is **not** stored on the webserver!) but this method is rather simple, especially if you do not change your website that much!

## How ?

{{% alert note %}}
Assumptions:

- Your webpage URL is `https://website.com/~username/`
- On the webserver, your public folder is named `~/public_html`
{{% /alert %}}

At the root of your website source code (on your computer), type the following commands in a terminal (the second line must obviously be modified accordingly):

```bash
hugo
rsync -avz --delete public/ username@webserver:~/public_html
```

The first command, `hugo`, creates a `public` folder containing the website. The second command, `rsync`, synchronizes the folders `public` and the remote one. 

{{% alert note %}}
- The `scp` command is not recommended because it does not remove deprecated files: if you decided to unpublish a document, it will not be erased and thus will still be published!
- You can use a FTP software instead [such as Filezilla](https://filezilla-project.org/)
{{% /alert %}}

## Scripting

These two commands can be obviously merged in a script, for example:

```bash
#!/usr/bin/env bash
# deploy.sh
hugo
rsync -avz --delete public/ username@webserver:~/public_html
```
That way, every time you want to upload your modification, you simply have to launch the script:
```bash
sh deploy.sh
```

## SSH keys: login without password

You may have to type your password everytime you update your website. If that is the case, I highly recommend you [to use SSH keys](http://www.linuxproblem.org/art_9.html). It is quite simple to do yet very convenient.