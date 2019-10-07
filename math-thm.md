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

You may have see that my course are online, no pdf files but directly as webpages. I explain here how to achieve a similar result, using `hugo` and the `Academic` theme.

The `Academic` theme provides a [nice layout (=design) for documentation](https://sourcethemes.com/academic/docs/writing-markdown-latex/). The math expression can be written mostly as in a basic $\LaTeX$ file thanks to MathJax (just set `math = true` in the frontmatter of your `.md` file). Some features were however missing for a math course, especially the "AMS Theorem environment" of $\LaTeX$.

## Features

I have developped a "`thm` package" written as [Hugo shortcodes](https://gohugo.io/content-management/shortcodes/#readout) to mimic it. A shortcode is a portion of code that `Hugo` will escape from the Markdown, making it possible to call external functions inside the Markdown. It features

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

## Installing it

### Installing

1. In your website root folder, type
  ```
  mkdir -p layouts/partials/shortcodes i18n assets/css
  git clone https://github.com/Bertbk/hugo-thm.git
  cp -r hugo-thm/thm layouts/partials/shortcodes/thm
  cp -r hugo-thm/i18n i18n/thm
  cp hugo-thm/css/thm.css assets/css/thm.css
  rm -rf hugo-thm
  ```
2. In `config/_default/params.toml` file, force `hugo` to load the `css` file
  ```toml
  plugins_css = ["thm"]
  ```


That's it! If you work locally with `hugo serve` you might be force to relaunch it (quit and relaunch).

To deploy your website with this package, do not forget to add the new files to git.

### Update

To update this package, the best think to do is, sadly, to "re-do" the installation process and override the files.

### Customisation

If you know a little bit about the CSS then is it quite easy, you juste have to change `thm.css` file. If you do not know about CSS but want to change the colors, no problem, have a look at `thm.css` file and seach for the colors, you will quickly understand how it works.