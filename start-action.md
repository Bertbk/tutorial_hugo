+++
title = "Time for Action"

date = 2019-09-30T00:00:00
# lastmod = 2018-09-09T00:00:00

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

math = false
weight = 10
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
  name = "Time for Action"
  parent = "I. Getting Started"
  identifier = "start"
  weight = 10
  url=""

+++

{{% alert note %}}
If you do not find the information you want, please have a look at the exhaustive and up to date [documentation of the Academic theme](https://sourcethemes.com/academic/docs/install).
{{% /alert %}}

## Installation

Create a folder for your source code. For example in `~/Documents/website` (not in `~/public_html`!) and there, type:

```bash
git clone https://github.com/sourcethemes/academic-kickstart.git professional
cd professional
git submodule update --init --recursive
hugo serve
```
This will launch a local web server. In your favorite browser (firefox, chrome, ~~edge~~, ...) go to [http://localhost:1313](http://localhost:1313): you should get a website talking about the Academic theme, something like the image below:

{{< figure src="../splashscreen.png" title="Splashscreen (possibly different)" >}}

## Customization

Now you definitely want to customize our website! Prior to that, lets just have a few words about the folders composing your repository:

- `config/_default/`: Starts here: open the configuration files there and changes the meta-data as you want
- `content/`: This is where the content of your website is stored, in the form of markdown files
  - `content/home`: Homepage, every `.md` file (except `index`) is a *widget* that you can activate or not
  - `content/post`: Your Post messages (blog)
  - `content/project`: Your projects
  - `content/publication`: Your scientific papers
  - `content/talk`: Your talks
- `static/`: Local files (image, ...) that will be available online

Finally, **never modify** files located in `themes/academic` folder! Otherwise, you will not be able to get updates. The `themes/academic/exampleSite` folder is great to get up-to-date examples, though!

You should now go to the [documentation of the Academic theme](https://sourcethemes.com/academic/docs) to get a nice and customed webpage.

## Hugo : tips & tricks

### Base URL

In `config/_default/config.toml`, there is a line for the `baseurl` option:
```toml
baseurl = "/"
```
There you **must** provide the *base url* of your website. For example, if your website is hosted at `https://my-lab/users/~me/` then you should copy paste that URL into `baseurl`:

```toml
baseurl = "https://my-lab/users/~me/"
```
This helps hugo to search for the file in the right place, especially the `.css` file (design)!

### Structure

Basically, the structure of your `content/` folder will be kept in your future website:

{{< diagram >}}
graph LR
    A("<code>content/projet/hello/index.md</code>") -->|<code>hugo</code>|B(<code>website.com/project/hello</code>)
{{< /diagram >}}

You can hence add custom folders and files in your `content` folder (you are **not** restricted by the theme!). 

A good idea though, is to keep the [page bundle system](https://gohugo.io/content-management/page-bundles/): one folder per "page". For example, if you want to add a page, say `website.com/legal`, declaring the Legal Notice of your website, you can create a folder and file at `content/legal/index.md`.


