+++
title = "Thm Environment"

date = 2019-09-30T00:00:00
# lastmod = 2018-09-09T00:00:00

draft = false  # Is this a draft? true/false
toc = true  # Show table of contents? true/false
type = "docs"  # Do not modify.

math = true
weight = 200
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
  name = "Thm Environment"
  parent = "III. Math Course"
  identifier = "math"
  weight = 200
  url=""

+++

<a href="https://github.com/Bertbk/hugo-thm"><button type="button" class="btn btn-outline-primary"><i class="fab fa-github"></i> Download hugo-thm on Github</button></a>

You may have see that my course are online, no pdf files but directly as webpages. I explain here how to achieve a similar result, using `hugo` and the `Academic` theme.

The `Academic` theme provides a [nice layout (=design) for documentation](https://sourcethemes.com/academic/docs/writing-markdown-latex/). The math expression can be written mostly as in a basic $\LaTeX$ file thanks to MathJax (just set `math = true` in the frontmatter of your `.md` file). Some features were however missing for a math course, especially the "AMS Theorem environment" of $\LaTeX$.

## Features

I have developped a ["`thm` package"](https://github.com/Bertbk/hugo-thm) written as [Hugo shortcodes](https://gohugo.io/content-management/shortcodes/#readout) to mimic it. A shortcode is a portion of code that `Hugo` will escape from the Markdown, making it possible to call external functions inside the Markdown. It features

- Customizable design
- Different type: Theorem, Proposition, Lemma, Corollary, Definition
- Theorem naming
- Cross reference
- Multi languages
- Proof environment
- Auto numbering (using CSS)

## Example

### Thm blocks

```md
{{</* thm/thm type="theorem" name="of me" label="thm:me"*/>}}
This theorem proves that covfefe.
{{</* /thm */>}}
{{</* thm/proof */>}}
The proof is very good. I like proof. I have big proof.
{{</* /thm/proof */>}}
```

leads to this

{{< thm/thm type="theorem" name="of me" label="thm:me" >}}
This theorem proves that covfefe.
{{< /thm/thm >}}
{{< thm/proof >}}
The proof is very good. I like proof. I have big proof.
{{< /thm/proof >}}

You can change `type="theorem"` by `proposition`, `lemma`, `corollary` or `definition`.

### Cross reference

A "theorem" can moreover be referenced using `thm/ref` using three different ways:

1. **Inline implicite** (order of arguments matters) :
  ```md
  Personally, my favorite is the {{</* thm/ref "thm:me" "covfefe Theorem" /*/>}}.
  ```
  Personally, my favorite is the {{< thm/ref "thm:me" "covfefe Theorem" />}}.
2. **Inline explicite**  (order of arguments does not matter!):
  ```md
  Personally, my favorite is the {{</* thm/ref ref="thm:me" text="covfefe Theorem" /*/>}}.
  ```
  Personally, my favorite is the {{< thm/ref ref="thm:me" text="covfefe Theorem" />}}.
3. **Environment**:
  ```md
  Personally, my favorite is the {{</* thm/ref "thm:me"*/>}}covfefe Theorem{{</* /thm/ref */>}}.
  ```
  Personally, my favorite is the {{< thm/ref "thm:me">}}covfefe Theorem{{< /thm/ref >}}.

{{% alert note %}}
As you notice and contrary to $\LaTeX$, the cross reference do not provide the number of the theorem. This is a little bit complicated as the numbering is done through CSS counter and I believe it is not necessary. However, if you are interested in, we can discuss about it. 
{{% /alert %}}

## Installation

There are 2.5 ways of installing it:

1. As a theme (simplest, recommended), through...
  - ... Direct download (non `git` users)
  - ... `git` submodule (updatable, customisable)
2. As a Go module (easy but not customisable)

### As a Theme

1. Add `"hugo-thm"` as a theme in `config/_default/config.toml`. Place it after `"academic"` (order matters):
    ```toml
    #params.toml
    # Name of Academic theme folder in `themes/`.
    theme = ["academic", "hugo-thm"]
    ```
2. If your academic version is...
  - Greater than v4.6: create (if not already done) a file in `assets/scss/custom.scss` and add this line
    ```scss
    @import "thm";
    ```
  - Less than v4.6: Add `"thm"` to `plugins_css` in `config/_default/params.toml`:
    ```toml
    # params.toml
    plugins_css = ["thm"]
    ```

You now have to download the "theme" using one of these way:

1. Direct Download :
   - Download [the last version](https://github.com/Bertbk/hugo-thm/archive/master.zip)
   - Extract and place `hugo-thm` folder in your `themes` folder
2. Git submodule. At the root your folder, type the following command
    ```bash
    git submodule add https://github.com/Bertbk/hugo-thm.git themes/hugo-thm
    ```

{{% alert note %}}
Some remarks:

- To use `git submodule`, your folder must also be a git repo!
- Do not forget to commit/add `.gitmodules`
- If you have set SSH key then you can use `ssh` instead of `https`:
    ```bash
    git submodule add git@github.com:Bertbk/hugo-thm.git themes/hugo-thm
    ```
  You can modify the `.gitmodules` file accordingly. 
- If, in addition to SSH, your website is automatically build through Gitalb page. You might need to add your ssh key to Gitlab variable and mofidy your `.gitlab-ci`.
{{% /alert %}}

### (Hu)Go Module

Add the following line at the end of your `config/_default/config.toml`:
```toml
#config.toml
# Modules
[module]
  proxy = "direct"
  
  [[module.imports]]
    disable = false
    ignoreConfig = false
    path = "github.com/Bertbk/hugo-thm"
```

Then type the following commands at the root of your folder
```
hugo mod init `pwd`
hugo mod get -u
```

{{% alert note %}}
If you use Gitlab Page, you must add these line in your `.gitlab-ci.yml`
{{% /alert %}}

## Customization

If you know a little bit about the CSS then is it quite easy, the main file being `assets/scss/thm.scss`. If you do not know about CSS but want to change the colors, no problem, have a look at `assets/scss/thm.scss` file and search for the colors, you will quickly understand how it works.

{{% alert note %}}
It seems that the css file are hidden when installing this package as a Go Module.
{{% /alert %}}