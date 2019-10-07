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

You do not want to use `git` and Gitlab? In that case, you can still deploy your website *manually*. Even if I would recommend the usage of `git` and a git server, I can understand that you prefer to use this manual method, especially if your website does not change that much!

{{% alert note %}}
With this method, `git` is no more mandatory but remember that `git` helps you manage your history of files and, as a side effect, it creates a backup of your code on a remote server: if your computer crash, you will not be able to recover the code that has been used to build your website!
{{% /alert %}}

## Build the website 

Simply type the following command:

```bash
hugo
```

This create a `public` folder containing the website. You just now needs to send everything to the remote server.

## Sending to server

{{% alert note %}}
I assume that:

- The url of your webpage is `https://website.com/~myaccount/`
- On the webserver, the public folder is named `~/public_html`

Adapt the following steps to your case is needed. 
{{% /alert %}}

You can use `scp` to send the files to the remote, however, `scp` will override updated files but not remove the potential deprecated files: if you decided to unpublish a document, it will still be published! I suggest you use the `rsync` command instead:

```bash
rsync -avz --delete public/ username@webserver:~/public_html
```

## Summary and script template

Here is a template for a script that does the two operation above. Copy it on the root of your website source code, adapt it and simply launch it everytimes you want to build and deploy your website!

```bash
#!/usr/bin/env bash
# deploy.sh
hugo
rsync -avz --delete public/ username@webserver:~/public_html
```
And then, if the file is named `deploy.sh`, you simply have to type
```bash
sh deploy.sh
```

## SSH keys: login without password

You may have to type your password everytime you update your website. If that is the case, I highly recommend you [to use SSH keys](http://www.linuxproblem.org/art_9.html).