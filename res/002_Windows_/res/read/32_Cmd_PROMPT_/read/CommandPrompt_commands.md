## [_GUIDES_][1] > [Windows][3]  > 3. SYS. SOFTWARE > 2. SERVICES > **Command Prompt (CMD)**

## <p align=center>[Git & GitHub][2] | [Windows][3] | [Linux][4] | [Networks][5] <br/> [Programming][6] | [Databases][7] | [Docker & Kubernetes][8] | [Embedded systems][9] </p>

<!--
* [_GUIDES_][1]
* [Git & GitHub][2]
* [Windows][3]
* [Linux][4]
* [Networks][5]
* [Programming][6]
* [Databases][7]
* [Docker & Kubernetes][8]
* [Embedded systems][9]
-->

[1]: ../../../../../../README.md
[2]: ../../../../../001_Git_and_GitHub_/Git_And_GitHub.md
[3]: ../../../../Windows.md
[4]: ../../../../../003_Linux_(Unix)_/Linux_(Unix).md
[5]: ../../../../../004_Networks_/Networks.md
[6]: ../../../../../005_Programming_languages_/Programming.md
[7]: ../../../../../006_Databases_/Databases.md
[8]: ../../../../../007_Docker_and_Kubernetes_/Docker_and_Kubernates.md
[9]: ../../../../../008_Embedded_systems_/Embedded_systems.md

--- 
<br/>
<!-- ---------------------------------- * Navigation * ---------------------------------- -->

# <p align=center><b>Command Prompt (CMD) Commands</b> <i>(Chaet sheet)</i></p>

## CONTENTS:
* Comandlets
* Scripts

<!--
## CONTENTS:
* Headers
* Emphasis
* Lists
* Images
* Links
* Blockquotes
* Inline code
* GitHub Flavored Markdown
* Syntax highlighting *(See: [List of language aliases][10])*
* Task Lists
* Tables
* SHA references
* Issue references within a repository
* Username `@mentions`
* Strikethrough
* Emoji
 
---
<br/>

# Syntax guide
Markdown is a way to style text on the web. You control the display of the document; formatting words as bold or italic, adding images, and creating lists are just a few of the things we can do with Markdown. Mostly, Markdown is just regular text with a few non-alphabetic characters thrown in, like # or *.

You can use Markdown most places around GitHub:
* [Gists][11]
* Comments in Issues and Pull Requests
* Files with the `.md` or `.markdown` extension
For more information, see "[Writing on GitHub][12]" in the GitHub Help.

Here’s an overview of Markdown syntax that you can use anywhere on GitHub.com or in your own text files.

---
<br/>

## Headers
### Example:
```pandoc
# This is an <h1> tag
## This is an <h2> tag
### This is an <h3> tag
#### This is an <h4> tag
##### This is an <h5> tag
###### This is an <h6> tag
```

#### *`Would become (result)`*:
# This is an \<h1> tag
## This is an \<h2> tag
### This is an \<h3> tag
#### This is an \<h4> tag
##### This is an \<h5> tag
###### This is an \<h6> tag

---
<br/>

## Emphasis
You can use an asterisk or an underscore (both apply).
Use one character for *Italic*, double character - **Bold**

### Example:
```pandoc
*This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

_You **can** combine them_
```

#### *`Would become (result)`*:
*This text will be italic* <br/>
_This will also be italic_

**This text will be bold** <br/>
__This will also be bold__

_You **can** combine them_

---
<br/>

## Lists
### Example:
```pandoc
// Unordered List
* Item 1     // There must be an indent between the asterisk and the first character
* Item 2
  * Item 2a  // Before the asterisk must be indented by 3 spaces
  * Item 2b

// Ordered List
1. Item 1     // After the number must be a dot
2. Item 2
3. Item 2
  1. Item 2a
  2. Item 2b
```

#### *`Would become (result)`*:
### Unordered List
* *Item 1*
* *Item 2*
  * *Item 2a*
  * *Item 2b*

<br/>

### Ordered List:
1. *Item 1*
2. *Item 2*
3. *Item 3*
   1. *Item 3a*
   2. *Item 3b*

---
<br/>

## Images
Syntax:
<br/>
**!\[** <*Alt Text*> **]\(** <*url*> **)**
<br>
or
<br/>
**!\[** <*Alt Text*> **]\[** <*link number*> **]**
<br/>
**\[**<*link number*>**]:** \<*url*>
<br>

### Example:
```pandoc
// Variant 1:
![MarkDown Logo](../img/MarkDownLogo.png)

// Variant 2:
![MarkDown Logo][5]
    // ... some text ...
[5]: ../img/MarkDownLogo.png
```

#### *`Would become (result)`*:
![MarkDown Logo](../img/MarkDownLogo.png)

---
<br/>

## Links
### Automatic linking URLs
Any URL (like https://github.com) will be automatically converted into a clickable link. There is nothing to do.
<br/>

### Manually linking URLs
Syntax:
<br/>
**\[** <*Alt Text*> **]\(** <*url*> **)**
<br>
or
<br/>
**\[** <*Alt Text*> **]\[** <*link number*> **]**
<br/>
**\[**<*link number*>**]:** \<*url*>
<br>

### Example:
```pandoc
// Variant 1 (Ordinary url): 
https://github.com

// Variant 2 (Text as link): 
[GitHub](https://github.com)

// Variant 3 (Text as link with internal link): 
[GitHub][13]
    // ... some text ...
[13]: https://github.com
```

#### *`Would become (result)`*:
*Automatic linking:*<br/>
https://github.com
<br/>

*Manually linking:*<br/>
[GitHub](https://github.com)

[GitHub][13]'s leverage automatic Markdown rendering

[GitHub][13]’s apply unique Markdown extensions

[13]: https://github.com 

---
<br/>

## Blockquotes
### Example:
```pandoc
As Kanye West said:
> We're living the future so
> the present is our past.
```
#### *`Would become (result)`*:
As Kanye West said:
> We're living the future so
> the present is our past.

---
<br/>

## Inline code
### Example:
```pandoc
I think you should use an `<addr>` element here instead.
```
#### *`Would become (result)`*:
I think you should use an `<addr>` element here instead.

---
<br/>

## GitHub Flavored Markdown
GitHub.com uses its own version of the Markdown syntax that provides an additional set of useful features, many of which make it easier to work with content on GitHub.com.

> ***Note***: that some features of *GitHub Flavored Markdown* are only available in the descriptions and comments of Issues and Pull Requests. These include @mentions as well as references to SHA-1 hashes, Issues, and Pull Requests. Task Lists are also available in Gist comments and in Gist Markdown files.

---
<br/>

## Syntax highlighting
Here’s an example of how you can use syntax highlighting with [GitHub Flavored Markdown][14]:

### See [List of language aliases][15] that provide syntax highlighting in the next conctruction:

```pandoc
``` <Alias for Markdown>

      ... code ...

'``
```

### Example:
```javascript
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
```

### You can also simply indent your code by four spaces:
```javascript
    function fancyAlert(arg) {
      if(arg) {
        $.facebox({div:'#foo'})
      }
    }
```

### Here’s an example of Python code `without` syntax highlighting:
```
def foo():
    if not bar:
        return True
```

### Here’s `with` syntax highlighting:
```python
def foo():
    if not bar:
        return True
```

---
<br/>

## Task Lists
### Example:
```pandoc
- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
- [x] list syntax required (any unordered or ordered list supported)
- [x] this is a complete item
- [ ] this is an incomplete item
```
If you include a task list in the first comment of an Issue, you will get a handy progress indicator in your issue list. It also works in Pull Requests!

#### *`Would become (result)`*:
- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
- [x] list syntax required (any unordered or ordered list supported)
- [x] this is a complete item
- [ ] this is an incomplete item

---
<br/>

## Tables
You can create tables by assembling a list of words and dividing them with hyphens `-` (for the first row), and then separating each column with a pipe `|`:

### Example:
```pandoc
First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column
```

#### *`Would become (result)`*:
First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column

---
<br/>

## SHA references
Any reference to a commit's [SHA-1 hash][16] will be automatically converted into a link to that commit on GitHub.

### Example:
```
16c999e8c71134401a78d4d46435517b2271d6ac
mojombo@16c999e8c71134401a78d4d46435517b2271d6ac
mojombo/github-flavored-markdown@16c999e8c71134401a78d4d46435517b2271d6ac
```
#### *`Would become (result)`*:
16c999e8c71134401a78d4d46435517b2271d6ac
mojombo@16c999e8c71134401a78d4d46435517b2271d6ac
mojombo/github-flavored-markdown@16c999e8c71134401a78d4d46435517b2271d6ac

---
<br/>

## Issue references within a repository
Any number that refers to an Issue or Pull Request will be automatically converted into a link.

### Example:
```
#1
github-flavored-markdown#1
yoricsv/github-flavored-markdown#1
```
#### *`Would become (result)`*:
#1
github-flavored-markdown#1
yoricsv/github-flavored-markdown#1

---
<br/>

## Username @mentions
Typing an ``@`` symbol, followed by a username, will notify that person to come and view the comment. This is called an `@mention`, because you're *mentioning* the individual. You can also @mention teams within an organization.

---
<br/>

## Strikethrough
Any word wrapped with two tildes will appear **crossed out**

### Example:
```pandoc
~~this is some text~~
```

#### *`Would become (result)`*:
~~this is some text~~

---
<br/>

## Emoji
GitHub supports [emoji][17]

To see a list of every image we support, check out the [Emoji Cheat Sheet][18].

### Example:
ico | shortcode | ico | shortcode
--- | --- | --- | ---
:grinning: | \:grinning: | :smiley: | \:smiley:
:smile: | \:smile: | :grin: | \:grin:
:laughing: | \:laughing: | :sweat_smile: | \:sweat_smile:
:rofl: | \:rofl: | :joy: | \:joy:
:slightly_smiling_face: | \:slightly_smiling_face: | :wink: | \:wink:
:stuck_out_tongue_winking_eye: | \:stuck_out_tongue_winking_eye: | :zany_face: | \:zany_face:
:collision: | \:collision: | :bomb: | \:bomb:
:zzz: | \:zzz: | :smiley: | \:smiley:
:+1: | \:+1: | :-1: | \:-1:
:hourglass: | \:hourglass: | :zap: | \:zap:
:mute: | \:mute: | :loud_sound: | \:loud_sound:
:chart: | \:chart: | :memo: | \:memo:
:file_folder: | \:file_folder: | :chart_with_upwards_trend: | \:chart_with_upwards_trend:
:lock: | \:lock: | :unlock: | \:unlock:
:key: | \:key: | :hammer: | \:hammer:
:link: | \:link: | :toolbox: | \:toolbox:
:gear: | \:gear: | :wrench: | \:wrench:
:adhesive_bandage: | \:adhesive_bandage: | :smoking: | \:smoking:
:warning: | \:warning: | :no_entry: | \:no_entry:
:radioactive: | \:radioactive: | :biohazard: | \:biohazard:
:heavy_plus_sign: | \:heavy_plus_sign: | :heavy_minus_sign: | \:heavy_minus_sign:
:heavy_multiplication_x: | \:heavy_multiplication_x: | :heavy_division_sign: | \:heavy_division_sign:
:bangbang: | \:bangbang: | :question: | \:question:
:heavy_check_mark: | \:heavy_check_mark: | :x: | \:x:
:triangular_flag_on_post: | \:triangular_flag_on_post: | :electron: | \:electron:
:atom: | \:atom: | :octocat: | \:octocat:
:trollface: | \:trollface: | :recycle: | \:recycle:

<!--
* [List of language aliases][10]
* [Gists][11]
* [Writing on GitHub][12]
* [GitHub][13]
* [GitHub Flavored Markdown][14]
* [List of language aliases][15]
* [SHA-1 hash][16]
* [emoji][17]
-->

[10]: MarkDown_syntax_higlight_(short).md
[11]: https://gist.github.com/
[12]: https://help.github.com/categories/writing-on-github/
[13]: https://github.com 
[14]: https://help.github.com/articles/basic-writing-and-formatting-syntax/
[15]: MarkDown_syntax_higlight_(short).md
[16]: http://en.wikipedia.org/wiki/SHA-1
[17]: https://help.github.com/articles/basic-writing-and-formatting-syntax/#using-emoji
[18]: https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md

<!--Done!--> 

---
<br/>
