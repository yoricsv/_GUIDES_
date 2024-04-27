# [GUIDES](../../../../../README.md) -> [Git & GitHub](../../../Git_And_GitHub.md) -> __MarkDown *(Cheat-sheet)*__

<!-- ## <p align = center>[Git & GitHub][git] | [Windows][win] | [Linux][linux] | [Networks][nets] </br> [Programming][progLang] | [Databases][db] | [Docker & Kubernetes][docker] | [Embedded systems][embSys] | [CMake][CMake] </p> -->

## __List of Guides__

| Guide Name                    |   |  Guide Name                   |   | Guide Name                    |
|-------------------------------|---|-------------------------------|---|-------------------------------|
| [Windows][navWin]             | * | [Linux][navNix]               | * | [Networks][navNet]            |
| [Databases][navDBs]           | * | [Programming][navPLn]         | * | [Git & GitHub][navGit]        |
| [CMake][navCMk]               | * | [Docker & Kubernetes][navDkr] | * | [Embedded systems][navEmS]    |

[navWin]:   ../../../../002_Windows_/Windows.md
[navNix]:   ../../../../003_Linux_(Unix)_/Linux_(Unix).md
[navNet]:   ../../../../004_Networks_/Networks.md
[navDBs]:   ../../../../006_Databases_/Databases.md
[navPLn]:   ../../../../005_Programming_languages_/Programming.md
[navGit]:   ../../../Git_And_GitHub.md
[navCMk]:   ../../../../009_CMake_/CMake_Tutorial.md
[navDkr]:   ../../../../007_Docker_and_Kubernetes_/Docker_and_Kubernates.md
[navEmS]:   ../../../../008_Embedded_systems_/Embedded_systems.md

---
<!-- ---------------------------------- * Navigation * ---------------------------------- -->
<!-- TOC -->
- [GUIDES -\> Git \& GitHub -\> __MarkDown *(Cheat-sheet)*__](#guides---git--github---markdown-cheat-sheet)
  - [__List of Guides__](#list-of-guides)
    - [CONTENTS](#contents)
  - [__Syntax guide__](#syntax-guide)
  - [__Headers__](#headers)
        - [This is an `<h5>` tag](#this-is-an-h5-tag)
          - [This is an `<h6>` tag](#this-is-an-h6-tag)
  - [__Emphasis__](#emphasis)
  - [__Lists__](#lists)
  - [__Images__](#images)
  - [__Links__](#links)
    - [Automatic linking URLs](#automatic-linking-urls)
    - [Manually linking URLs](#manually-linking-urls)
  - [__Blockquotes__](#blockquotes)
  - [__Inline code__](#inline-code)
  - [__GitHub Flavored Markdown__](#github-flavored-markdown)
  - [__Syntax highlighting__](#syntax-highlighting)
    - [See List of language aliases that provide syntax highlighting in the next conctruction](#see-list-of-language-aliases-that-provide-syntax-highlighting-in-the-next-conctruction)
    - [You can also simply indent your code by four spaces](#you-can-also-simply-indent-your-code-by-four-spaces)
    - [Here’s an example of Python code `without` syntax highlighting](#heres-an-example-of-python-code-without-syntax-highlighting)
    - [Here’s `with` syntax highlighting](#heres-with-syntax-highlighting)
  - [__Task Lists__](#task-lists)
  - [__Tables__](#tables)
  - [__SHA references__](#sha-references)
  - [__Issue references within a repository__](#issue-references-within-a-repository)
  - [__Username @mentions__](#username-mentions)
  - [__Strikethrough__](#strikethrough)
  - [__Emoji__](#emoji)
<!-- TOC -->
<!--### CONTENTS

- Headers
- Emphasis
- Lists
- Images
- Links
- Blockquotes
- Inline code
- GitHub Flavored Markdown
- Syntax highlighting *(See: [List of language aliases][aliases])*
- Task Lists
- Tables
- SHA references
- Issue references within a repository
- Username `@mentions`
- Strikethrough
- Emoji
-->

## __Syntax guide__

Markdown is a way to style text on the web. You control the display of the document; formatting words as bold or italic, adding images, and creating lists are just a few of the things we can do with Markdown. Mostly, Markdown is just regular text with a few non-alphabetic characters thrown in, like # or *.

You can use Markdown most places around GitHub:

- [Gists][gist]
- Comments in Issues and Pull Requests
- Files with the `.md` or `.markdown` extension

For more information, see ["Writing on GitHub"][writing] in the GitHub Help.

Here’s an overview of Markdown syntax that you can use anywhere on GitHub.com or in your own text files.

## __Headers__

Example

```md
# This is an <h1> tag
```

> __Result:__
>
> # This is an `<h1>` tag

```md
## This is an <h2> tag
```

> __Result:__
>
> ## This is an `<h2>` tag

```md
### This is an <h3> tag
```

> __Result:__
>
> ### This is an `<h3>` tag

```md
#### This is an <h4> tag
```

> __Result:__
>
> #### This is an `<h4>` tag

```md
##### This is an <h5> tag
```

> __Result:__
>
> ##### This is an `<h5>` tag

```md
###### This is an <h6> tag
```

###### This is an `<h6>` tag

## __Emphasis__

You can use an asterisk or an underscore (both apply).
Use one character for *Italic*, double character - __Bold__

Example

```md
*This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

*You __can__ combine them*
```

> __Result:__
>
> *This text will be italic*
>
> _This will also be italic_
>
> **This text will be bold**
>
> __This will also be bold__
>
> *You __can__ combine them*

## __Lists__

Example

```pandoc
// Unordered List
- Item 1     // There must be an indent between the asterisk and the first character
- Item 2
  - Item 2a  // Before the asterisk must be indented by 3 spaces
  - Item 2b

// Ordered List
1. Item 1     // After the number must be a dot
2. Item 2
3. Item 2
  1. Item 2a
  2. Item 2b
```

> __Result:__
>
> Unordered List:
>
> - *Item 1*
> - *Item 2*
>   - *Item 2a*
>   - *Item 2b*
>
> Ordered List:
>
> 1. *Item 1*
> 2. *Item 2*
> 3. *Item 3*
>    1. *Item 3a*
>    2. *Item 3b*

## __Images__

Syntax

__!\[__ <*Alt Text*> __]\(__ <*url*> __)__

or

__!\[__ <*Alt Text*> __]\[__ <*link number*> __]__

__\[__<*link number*>__]:__ \<*url*>

```pandoc
# __Vagrant__

<!-- Use attribute style -->
<img alt   = "Vagrant"
     src   = "../img/vagrant.svg"
     style = "width:150px"
/>

<!-- Use attribute width -->
<img alt   = "Vagrant"
     src   = "../img/vagrant.svg"
     width = "150px"
/>

<!-- Use style css -->
![Vagrant](../img/vagrant.svg)

<img alt   = "vagrant"
     class = "image_width-150px"
     src   = "../img/vagrant.svg"
/>

<style>
    img[alt = "Vagrant"] {
        width: 150px;
    }
    .image_width-150px {
        width: 150px;
    }
</style>
```

Example

```pandoc
// Variant 1:
![MarkDown Logo](../img/MarkDownLogo.png)

// Variant 2:
![MarkDown Logo][5]
    // ... some text ...
[5]: ../img/MarkDownLogo.png
```

> __Result:__
>
> ![MarkDown Logo](../img/MarkDownLogo.png)

---

## __Links__

### Automatic linking URLs

Any URL (like <https://github.com>) will be automatically converted into a clickable link. There is nothing to do.

### Manually linking URLs

Syntax

__\[__ <*Alt Text*> __]\(__ <*url*> __)__

or

__\[__ <*Alt Text*> __]\[__ <*link number*> __]__

__\[__<*link number*>__]:__ \<*url*>

Example

```pandoc
// Variant 1 (Ordinary url): 
<https://github.com>

// Variant 2 (Text as link): 
[GitHub](https://github.com)

// Variant 3 (Text as link with internal link): 
[GitHub][13]
    // ... some text ...
[13]: https://github.com
```

> __Result:__
>
> *Automatic linking:*
>
> <https://github.com>
>
> *Manually linking:*
>
> [GitHub](https://github.com)
>
> [GitHub][github]'s leverage automatic Markdown rendering
>
> [GitHub][github]’s apply unique Markdown extensions
>
> [github]: https://github.com

---

## __Blockquotes__

Example

```pandoc
As Kanye West said:

> We're living the future so
> the present is our past.
```

> __Result:__
>
> As Kanye West said:
>
> > We're living the future so
> > the present is our past.

---

## __Inline code__

Example

```pandoc
I think you should use an `<addr>` element here instead.
```

> __Result:__
>
> I think you should use an `<addr>` element here instead.

---

## __GitHub Flavored Markdown__

GitHub.com uses its own version of the Markdown syntax that provides an additional set of useful features, many of which make it easier to work with content on GitHub.com.

> __NOTE:__
>
> that some features of *GitHub Flavored Markdown* are only available in the descriptions and comments of Issues and Pull Requests. These include @mentions as well as references to SHA-1 hashes, Issues, and Pull Requests. Task Lists are also available in Gist comments and in Gist Markdown files.

---

## __Syntax highlighting__

Here’s an example of how you can use syntax highlighting with [GitHub Flavored Markdown][formatting]:

### See [List of language aliases][aliases] that provide syntax highlighting in the next conctruction

```pandoc
``` <Alias for Markdown>

      ... code ...

'``
```

Example

```javascript
function fancyAlert(arg)
{
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
```

### You can also simply indent your code by four spaces

```javascript
function fancyAlert(arg)
{
    if(arg)
    {
        $.facebox(
            {div:'#foo'}
        )
    }
}
```

### Here’s an example of Python code `without` syntax highlighting

```\
def foo():
    if not bar:
        return True
```

### Here’s `with` syntax highlighting

```python
def foo():
    if not bar:
        return True
```

---

## __Task Lists__

Example:

```pandoc
- [x] @mentions, #refs, [links](), __formatting__, and <del>tags</del> supported
- [x] list syntax required (any unordered or ordered list supported)
- [x] this is a complete item
- [ ] this is an incomplete item
```

If you include a task list in the first comment of an Issue, you will get a handy progress indicator in your issue list. It also works in Pull Requests!

> __Result:__
>
> - [x] @mentions, #refs, [links](MarkDown.md), __formatting__, and ~~tags~~ supported
> - [x] list syntax required (any unordered or ordered list supported)
> - [x] this is a complete item
> - [ ] this is an incomplete item

---

## __Tables__

You can create tables by assembling a list of words and dividing them with hyphens `-` (for the first row), and then separating each column with a pipe `|`:

Example

```pandoc
| First Header                  | Second Header                 |
|-------------------------------|-------------------------------|
| Content from cell 1           | Content from cell 2           |
| Content in the first column   | Content in the second column  |
```

> __Result:__
>
> | First Header                  | Second Header                 |
> |-------------------------------|-------------------------------|
> | Content from cell 1           | Content from cell 2           |
> | Content in the first column   | Content in the second column  |

---

## __SHA references__

Any reference to a commit's [SHA-1 hash][sha1] will be automatically converted into a link to that commit on GitHub.

Example

```bash
16c999e8c71134401a78d4d46435517b2271d6ac
mojombo@16c999e8c71134401a78d4d46435517b2271d6ac
mojombo/github-flavored-markdown@16c999e8c71134401a78d4d46435517b2271d6ac
```

> __Result:__
>
> 16c999e8c71134401a78d4d46435517b2271d6ac</br>
> mojombo@16c999e8c71134401a78d4d46435517b2271d6ac</br>
> mojombo/github-flavored-markdown@16c999e8c71134401a78d4d46435517b2271d6ac

## __Issue references within a repository__

Any number that refers to an Issue or Pull Request will be automatically converted into a link.

Example

```pandoc
#1
github-flavored-markdown#1
yoricsv/github-flavored-markdown#1
```

> __Result:__
>
> #1</br>
> github-flavored-markdown#1</br>
> yoricsv/github-flavored-markdown#1

## __Username @mentions__

Typing an `@` symbol, followed by a username, will notify that person to come and view the comment. This is called an `@mention`, because you're _mentioning_ the individual. You can also @mention teams within an organization.

## __Strikethrough__

Any word wrapped with two tildes will appear __crossed out__

Example

```pandoc
~~this is some text~~
```

> __Result:__
>
> ~~this is some text~~

---

## __Emoji__

GitHub supports [emoji][emoji]

To see a list of every image we support, check out the [Emoji Cheat Sheet][emojiCheat].

Example:

| ico                            | shortcode                        | ico                        | shortcode                    |
|--------------------------------|----------------------------------|----------------------------|------------------------------|
| :grinning:                     | `:grinning:`                     | :smiley:                   | `:smiley:`                   |
| :smile:                        | `:smile:`                        | :grin:                     | `:grin:`                     |
| :laughing:                     | `:laughing:`                     | :sweat_smile:              | `:sweat_smile:`              |
| :rofl:                         | `:rofl:`                         | :joy:                      | `:joy:`                      |
| :slightly_smiling_face:        | `:slightly_smiling_face:`        | :wink:                     | `:wink:`                     |
| :stuck_out_tongue_winking_eye: | `:stuck_out_tongue_winking_eye:` | :zany_face:                | `:zany_face:`                |
| :collision:                    | `:collision:`                    | :bomb:                     | `:bomb:`                     |
| :zzz:                          | `:zzz:`                          | :smiley:                   | `:smiley:`                   |
| :+1:                           | `:+1:`                           | :-1:                       | `:-1:`                       |
| :hourglass:                    | `:hourglass:`                    | :zap:                      | `:zap:`                      |
| :mute:                         | `:mute:`                         | :loud_sound:               | `:loud_sound:`               |
| :chart:                        | `:chart:`                        | :memo:                     | `:memo:`                     |
| :file_folder:                  | `:file_folder:`                  | :chart_with_upwards_trend: | `:chart_with_upwards_trend:` |
| :lock:                         | `:lock:`                         | :unlock:                   | `:unlock:`                   |
| :key:                          | `:key:`                          | :hammer:                   | `:hammer:`                   |
| :link:                         | `:link:`                         | :toolbox:                  | `:toolbox:`                  |
| :gear:                         | `:gear:`                         | :wrench:                   | `:wrench:`                   |
| :adhesive_bandage:             | `:adhesive_bandage:`             | :smoking:                  | `:smoking:`                  |
| :warning:                      | `:warning:`                      | :no_entry:                 | `:no_entry:`                 |
| :radioactive:                  | `:radioactive:`                  | :biohazard:                | `:biohazard:`                |
| :heavy_plus_sign:              | `:heavy_plus_sign:`              | :heavy_minus_sign:         | `:heavy_minus_sign:`         |
| :heavy_multiplication_x:       | `:heavy_multiplication_x:`       | :heavy_division_sign:      | `:heavy_division_sign:`      |
| :bangbang:                     | `:bangbang:`                     | :question:                 | `:question:`                 |
| :heavy_check_mark:             | `:heavy_check_mark:`             | :x:                        | `:x:`                        |
| :triangular_flag_on_post:      | `:triangular_flag_on_post:`      | :electron:                 | `:electron:`                 |
| :atom:                         | `:atom:`                         | :octocat:                  | `:octocat:`                  |
| :trollface:                    | `:trollface:`                    | :recycle:                  | `:recycle:`                  |

[gist]:       https://gist.github.com/
[writing]:    https://help.github.com/categories/writing-on-github/
[formatting]: https://help.github.com/articles/basic-writing-and-formatting-syntax/
[aliases]:    MarkDown_syntax_higlight_(short).md
[sha1]:       http://en.wikipedia.org/wiki/SHA-1
[emoji]:      https://help.github.com/articles/basic-writing-and-formatting-syntax/#using-emoji
[emojiCheat]: https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md
