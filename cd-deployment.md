+++
title = "Gitlab Page"

date = 2019-09-30T00:00:00
# lastmod = 2018-09-09T00:00:00

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

math = false
weight = 110
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
  name = "Gitlab Page"
  parent = "II. Continuous Delivery"
  identifier = "deployment"
  weight = 110
  url=""

+++

Your website looks amazing on your computer + you know how `git` works? Awesome, let's make the whole world knows how great your website (and you) is!

## `git push` to Gitlab (remote repository)

Currently, the remote server of your local repository is `https://github.com/sourcethemes/academic-kickstart.git`. You can see it by typing
```bash
git remote -v
> origin	https://github.com/sourcethemes/academic-kickstart.git (fetch)
> origin	https://github.com/sourcethemes/academic-kickstart.git (push)
```
We obviously want to change that. 

### Prepare the server

First, create an empty repository in your Gitlab's account. On the interface, click on `New Project` (top right) and then create a `blanck project`. The important point here is that the name of project matters a lot, **you must name it** using [Gitlab page convention](https://docs.gitlab.com/ee/user/project/pages/getting_started_part_one.html#gitlab-pages-domain-names). 


|GitLab server |	Name of the project| 	Website URL|
|---|---|---|
|Gitlab.com| 	username.gitlab.io 	|http(s)://username.gitlab.io|
|PLMLab.math.cnrs.fr| 	username.pages.math.cnrs.fr 	|http(s)://username.pages.math.cnrs.fr|

### Change the remote url

When your repository has been created, and in its main page, click on "clone" and copy/paste the "clone with ssh" line (you can use `https` but it slower and you have to ). It should be something like 
```bash
# If PLMLAB
git@plmlab.math.cnrs.fr:username/username.pages.math.cnrs.fr.git
# else if Gitlab.com
git@gitlab.com:username/username.gitlab.io.git
```
Back on the git repository, at the root of it, change the url of your remote and then push to your repo:
```bash
git remote set-url origin git@plmlab.math.cnrs.fr:username/username.pages.math.cnrs.fr.git
git push origin master
```
`git` might be unhappy and asks you to push using a different command: please do what it asks you to do, for example it can be the following command:
```bash
git push --set-upstream origin master
```

After refreshing your gitlab page on your browser, you should see your repository: the files, the name of last commit, ...

## Gitlab Page: Continuous Deployment (CD)

### Gitlab CI (Continuous Integration)

Your website is almost ready, you just need to explain `Gitlab` that it must build your website each times you push changes:

1. Depending on your webserver, download or copy/past the right `.gitlab-ci.yml` and place it at the root of your folder: 
   - PLMLab: {{< gist Bertbk 2e0d1a5bef4c7c575b3de482da43bc6b >}}
   - Gilab.com: [Repo](https://gitlab.com/pages/hugo/blob/master/.gitlab-ci.yml) or [Direct download](https://gitlab.com/pages/hugo/raw/master/.gitlab-ci.yml?inline=false)
2. In your Gitlab/PLMLab account and in the project of your website:
   1. `Settings` → `CI/CD`→ `Variables` add a new variable named `HUGO_BASEURL` with value the url of your website (*e.g.* `http://username.pages.math.cnrs.fr/`)
   2. `Settings` → `General`→ Expand the `Visibility, project features, permissions`. Enable `Page access control` to `everyone` (do not forget to `save changes`!)
3. Do a dummy modification in your code, commit and push to activate the runner of Gitlab

If everything works fine, you should be able to access your website at `https://username.pages.math.cnrs.fr` on your browser after, say, 5 to 10 minuts. If you did not received an error email and if your website is still unaccessible, you should try to

- Refresh your browser multiple times
- Clear the cache of your browser
- Try another browser

This is due to the fact that it takes time for a new website to be "known".

### Checking the process

You can check the process (pipeline and jobs) in your Gitlab's interface in `CI/CD` → `Jobs` (or directly at `https://plmlab.math.cnrs.fr/username/username.pages.math.cnrs.fr/-/jobs`)

## Set a SSH key to loggin without password

Every time you `push` your repo, you must type your password. Boring, right? SSH keys are the tools you need: please have a look at [the Gitlab documentation](https://docs.gitlab.com/ee/ssh/) which provides clear explanation.