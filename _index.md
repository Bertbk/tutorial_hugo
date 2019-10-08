+++
title = "Tools & Workflow"

date = 2019-09-30T00:00:00
# lastmod = 2018-09-09T00:00:00

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

math = false
weight = 1
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
  name = "Tools & Workflow"
  identifier = "intro"
  parent = "I. Getting Started"
  weight = 1
  url=""

+++

## Tools: Hugo and Academic

This website is built using these two open-source great tools:

1. **[<i class="fas fa-cogs"></i> Hugo](https://gohugo.io): the engine**, a static site generator. Kind of like the engine that transforms a `.tex` file to a `.pdf`. The language is not **LaTeX** but [**Markdown**](https://daringfireball.net), easier to learn yet less powerful.
2. **[<i class="fas fa-palette"></i> Academic](https://github.com/gcushen/hugo-academic/): the design**, a theme for `Hugo` (layout, design, ...). Roughly speaking, it's the `documentclass` and frontmatter of a `LaTeX` file.


The below diagram illustrates the workflow: 

{{< diagram >}}
graph LR
    C[<code>hugo</code><br>Build website] --> |Success| E(<code>rsync</code><br> Send to server)
{{< /diagram >}}

This workflow however assume that you have a webserver!

## Preparing your computer

[Hugo](https://gohugo.io/) is a static site generator: a software that creates website from source code. As said previously, it acts as ((Lua)La)TeX engine that transforms `.tex` file to a beautiful `.pdf` file.

{{< diagram >}}
graph LR
    A("Mardown (<code>.md</code>)") -->|<code>hugo</code>|B(HTML)
{{< /diagram >}}

To install it, please see the [documentation page](https://gohugo.io/getting-started/installing/) or, in short:

- On MacOs: install [`brew`](https://brew.sh/) and then type 
  ```bash
  brew install hugo
  ```
- On Linux (and Windows): Download binary from [the official releases](https://github.com/gohugoio/hugo/releases):
  - Search for the "extended" version, "linux 64 bit" and `.deb` file (*e.g* `hugo_extended_0.58.3_Linux-64bit.deb`)
  - In a terminal and in the folder type 
    ```bash
    sudo dpkg -i --force-overwrite hugo_extended_0.58.3_Linux-64bit.deb
    ```
