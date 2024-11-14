---
layout: default
---

# Markdown Guide
This is a cheatsheet on how to use Markdown to create clean readme files. Markdown files use the extension ***.md***. In particular, this cheatsheet focuses on GitHub flavor markdown. You can also use raw HTML!

# Headers
## Sub Header
### Sub-sub header
###### Smallest Header
Headers are created using the hash symbol: `# Header`. You can use up to six hash symbols.

# Text formatting

Normal text

*Italicize text* with single asterisk: `*texts*`

**Bold text** with double asterisks: `**text**`

***Bold and italicize text*** with triple asterisks: `***text***`

~~Strikethrough text~~ with double tilde: `~~text~~`

> This is a quote using the greater-than symbol: `> text`

`This a line of code in text with single backticks`

```` c
``` c
This is a block of code
With triple backticks before and after code

int test = 10;
for (i = 1; i<test; i++) {
  printf("%d\n", i);
}

```
````
You can also add syntax highlighting by specifying language after the first set of triple backticks.


# Images
You can also embed images. HTML formatting works too!

Example:

Markdown -- `![Image](/docs/images/example.png)`

HTML -- `<img src="/docs/images/example.png" width="45%" />`

<img src="/docs/images/example.png" width="45%" />


# Links
[Link titles](./) work with both URLs and relative paths. Example:

`[link title](http://link)`

`[link title](./path)`

# Lists
You can make both ordered and unordered lists as well as numerical lists. You can combine the two for nested lists by indenting appropriately.

* Item 2 -- `* Item 2`
  * Can also use `-` or `+` in place of asterisks
* Item 1 -- `* Item 1`
* Item 3 -- `* Item 3`

or

1. Item 1 -- `1. Item 1`
  - This list is ordered using numbers
2. Item 2 -- `2. Item 2`
3. Item 3 -- `3. Item 3`

# Tables

|Centered|Left Justified|Right Justified|
|:---:   | :---         |           ---:|
| 1      | 0xA90        | A             |
| 2      | 0xB90        | B             |
| 3      | 0xC90        | C             |

Notes:
* You must include a blank line before your table in order for it to correctly render.
* There must be at least three hyphens in each column of the header row.

# References
[GitHub Markdown Guide](https://guides.github.com/features/mastering-markdown/)

[GitHub Flavor Markdown](https://help.github.com/articles/basic-writing-and-formatting-syntax/)
