+++
title = "Overview"

date = 2019-09-30T00:00:00
# lastmod = 2018-09-09T00:00:00

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

math = false
weight = 99
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
  name = "Overview"
  parent = "II. Continuous Delivery"
  identifier = "cd-intro"
  weight = 99
  url=""

+++

## Automatisation

Using `git` and the Gitlab pages provide the following advantages:

- Automatic build of the website whenever a change of the source code is submitted
- Static website is hosted for free
- Source code is saved on remote server (backup)

To achieve this continuous delivery, two tools are now mandatory:

1. **[<i class="fa fa-code-branch"></i> Git](https://git-scm.com/): the savier**, a source control that manages changes to your **repository** (= your source files = your content). Changes can be compared between version.
2. **[<i class="fab fa-gitlab"></i> Gitlab](https://gitlab.com): the robot** Gitlab is software/service that saves git repositories. It can moreover be used for *continuous deployment* by automatically rebuilding and updating my website whenever I modify some content.

The interaction between all these tools and services are described by this diagram

{{< diagram >}}
graph LR
    A[fa:fa-laptop <code>git push</code><br>send source code] -->B(fab:fa-gitlab <strong>GitLab server</strong><br>Store. Launch script)
    B --> C[<code>hugo</code><br>Build website]
    C -->|Error| D(fa:fa-times-circle No change)
    C -->|Success| E(fa:fa-check-circle Website updated)
{{< /diagram >}}

This can be translated as follows. 

> I'm working locally on my computer, making change to the content of my website. Whenever I'm happy with these changes, I launch the `git push` commands that send them to the Gitlab server (like a huge copy/paste). Gitlab then executes the `hugo` commands to re-build the website. If the process has been validated then the website is updated (erasing the previous version). Otherwise, the website is not changed (still accessible!) and I receive a notification email: I then have to debug.

This whole process takes about 3 to 4 minuts to complete and I only had to send my changes to the Gitlab server.

A short description of each of these tools is provided below.

## Preparing your computer

### Git

`git` is probably already installed on your unix system (MacOs and Linux) but you can check by typing `git` in a shell:
```bash
git
```
For windows user, you might need [to install it](https://git-scm.com/download/win). [Tortoise Git](https://tortoisegit.org/) provides a nice graphical interface and is embedded in the folder explorer.

### Git Server

{{% alert note %}}
For french math scientists, instead of using Gitlab.com, you should create an account on [**PLMLab**](https://plmlab.math.cnrs.fr/), which is an up to date instance of Gitlab, managed by the [great PLM team](https://portail.math.cnrs.fr/).

Your (professional) website will have a (professional) url: `your_account.pages.math.cnrs.fr`.
{{% /alert%}}

This tutorial focuses on the open-source software [Gitlab](https://gitlab.com) but everything works quite the same for Github. You can have a look at the [academic theme documentation](https://sourcethemes.com/academic/docs/install/) that propose to combine [Github](https://gohugo.io/hosting-and-deployment/hosting-on-github/) with [Netlify](https://netlify.com).

You just have to create an account on your Gitlab's instance of your choice:

- [Gitlab.com](https://gitlab.com): create a  account. 
- [PLMlab](https://plmlab.math.cnrs.fr/): reserved for math french academic employees

{{% alert note %}}
Gitlab is both a service (gitlab.com) and an open-source software (Gitlab). When speaking about Gitlab, I mean any instance of it: Gitlab.com or PLMlab.math.cnrs.fr for example.
{{% /alert %}}