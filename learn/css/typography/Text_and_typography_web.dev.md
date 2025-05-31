# Text and typography  |  web.dev

**Source URL:** [https://web.dev/learn/css/typography?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Ftypography](https://web.dev/learn/css/typography?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Ftypography)  
**Last Updated:** 2025-05-23T01:08:24.052Z  
**Extracted:** 2025-05-31 16:58:10

---

# Text and typography | web.dev

##### [The CSS Podcast - 036: Text & Typography](https://thecsspodcast.libsyn.com/tcp036-v2)

Text is one of the core building blocks of the web.

When making a website, you don't necessarily need to style your text; HTML actually has some pretty reasonable default styling.

However, text will likely make up the majority of your website, so it's worthwhile to add some styling to spruce it up. By changing a few basic properties, you can significantly improve the reading experience for your users!

  CodePen Embed - Text | styled unstyled combined  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

In this module, we'll start with the `@font-face` rule, which lets you import custom fonts into your webpages. This ensures that you have the exact typography you need, independent of user-installed fonts.

Following that, we'll cover essential CSS font properties including `font-family`, `font-style`, `font-weight`, and `font-size`. These basics set the stage for manipulating text for both style and readability.

We'll also touch on paragraph-specific properties like `text-indent` and `word-spacing`, before concluding with advanced topics such as variable fonts and pseudo-elements, which further refine your typographic control.

Practical examples and tips will be provided throughout to solidify your understanding and application of these CSS techniques.

## The `@font-face` rule

The `@font-face` CSS at-rule is instrumental in web design, letting you specify and use custom fonts to display text. The beauty of `@font-face` is in its versatility: it lets you source fonts from a remote server, or from a font installed on the user's device.

### Syntax

```
@font-face {
  font-family: "Trickster";
  src:
    local("Trickster"),
    url("trickster-COLRv1.otf") format("opentype") tech(color-COLRv1),
    url("trickster-outline.otf") format("opentype"),
    url("trickster-outline.woff") format("woff")
}
```

### Descriptors

[`ascent-override`](https://developer.mozilla.org/docs/Web/CSS/@font-face/ascent-override)

Customizes the ascent metric, impacting the space above the baseline.

[`descent-override`](https://developer.mozilla.org/docs/Web/CSS/@font-face/descent-override)

Adjusts the descent metric, affecting the space below the baseline.

[`font-display`](https://developer.mozilla.org/docs/Web/CSS/@font-face/font-display)

Controls the font's display behavior depending on its download status.

[`font-family`](https://developer.mozilla.org/docs/Web/CSS/font-family)

Names the font for use within font-related properties.

[`font-stretch`](https://developer.mozilla.org/docs/Web/CSS/font-stretch)

Sets acceptable horizontal scaling, specified as a single value or range.

[`font-style`](https://developer.mozilla.org/docs/Web/CSS/font-style)

Defines the font style, supporting angle ranges for oblique styles.

[`font-weight`](https://developer.mozilla.org/docs/Web/CSS/font-weight)

Determines the font's weight or range of weights available.

[`font-feature-settings`](https://developer.mozilla.org/docs/Web/CSS/font-feature-settings)

Enables access to OpenType font features.

[`font-variation-settings`](https://developer.mozilla.org/docs/Web/CSS/font-variation-settings)

Provides fine-tuned control over variable font settings.

[`line-gap-override`](https://developer.mozilla.org/docs/Web/CSS/@font-face/line-gap-override)

Overrides the font's default line gap.

[`size-adjust`](https://developer.mozilla.org/docs/Web/CSS/@font-face/size-adjust)

Applies a scaling factor to the font's outline and metrics.

[`src`](https://developer.mozilla.org/docs/Web/CSS/@font-face/src)

Defines the font source, whether local or remote. This is required for the `@font-face` rule. Combining `url()` and `local()` within the `src` is a common strategy that uses a local font if available, reverting to a remote font file as a fallback. Browsers prioritize resources based on the order of declaration, so `local()` should typically precede `url()`.

[`unicode-range`](https://developer.mozilla.org/docs/Web/CSS/@font-face/unicode-range)

Limits the characters this font should be used for.

### Description

`@font-face` frees designers from the constraints of "web-safe" fonts by letting them use custom typography. The `local()` function's ability to search for a font on the user's device offers a seamless experience that doesn't necessarily depend on an internet connection.

### Font MIME types

| **Format** | **MIME Type** |
| --- | --- |
| TrueType | `font/ttf` |
| OpenType | `font/otf` |
| Web Open Font Format | `font/woff` |
| Web Open Font Format 2 | `font/woff2` |

### The difference between @font-face and font-family

In CSS, `@font-face` and `font-family` are often confused, but they serve distinct purposes.

As we've discussed, `@font-face` is a rule used to define any custom fonts you want to use in your web application. It tells the browser where to download the font, how to display it during loading (with the `font-display` property), and specifies which subset of characters to download (with the `unicode-range`).

In contrast, `font-family` is a CSS property used within a CSS rule to assign a particular font or a list of fonts to an element. The fonts listed under `font-family` can be web-safe fonts, system fonts, or custom fonts defined with `@font-face`.

To summarize, `@font-face` declares a font and gives it a name, and `font-family` applies this declared font to HTML elements.

Here's an example of using both:

```
<table>
  <thead>
    <tr>
      <th><p><pre>
@font-face {
  font-family: "CustomFont";
  src: url("customfont.woff2") format("woff2");
}

body {
  font-family: "CustomFont", Arial, sans-serif;
}
```

In this example, `@font-face` defines "CustomFont" and tells the browser where to find it. The `font-family` property then applies it to the body element, with Arial as a fallback if "CustomFont" isn't available.

## Change the typeface

Use [`font-family`](https://developer.mozilla.org/docs/Web/CSS/font-family) to change the typeface of your text.

The `font-family` property accepts a comma-separated list of strings, either referring to _specific_ or _generic_ font families. Specific font families are quoted strings, such as "Helvetica", "EB Garamond", or "Times New Roman". Generic font families are keywords such as `serif`, `sans-serif`, and `monospace` (find the [full list of options on MDN](https://developer.mozilla.org/docs/Web/CSS/font-family#values)). The browser will display the first available typeface from the provided list.

When using `font-family`, you should specify at least one generic font family in case the user's browser doesn't have your preferred fonts. Generally, the fallback generic font family should be similar to your preferred fonts: if using `font-family: "Helvetica"` (a sans-serif font family), your fallback should be `sans-serif` to match.

  CodePen Embed - Text | font-family  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Use italic and oblique fonts

Use [`font-style`](https://developer.mozilla.org/docs/Web/CSS/font-style) to set whether text should be italic or not. `font-style` accepts one of the following keywords: `normal`, `italic`, and `oblique`.

  CodePen Embed - Text | font-style  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Make text bold

Use [`font-weight`](https://developer.mozilla.org/docs/Web/CSS/font-weight) to set the "boldness" of text. This property accepts keyword values (`normal`, `bold`), relative keyword values (`lighter`, `bolder`), and numeric values (`100` to `900`).

The keywords `normal` and `bold` are equivalent to the numeric values `400` and `700`, respectively.

The keywords `lighter` and `bolder` are calculated relative to the parent element. See MDN's [Meaning of Relative Weights](https://developer.mozilla.org/docs/Web/CSS/font-weight#meaning_of_relative_weights) for a handy chart showing how this value is determined.

  CodePen Embed - Text | font-weight numbers  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Change the size of text

Use [`font-size`](https://developer.mozilla.org/docs/Web/CSS/font-size) to control the size of your text elements. This property accepts length values, percentages, and a handful of keyword values.

In addition to length and percentage values, `font-size` accepts some _absolute_ keyword values (`xx-small`, `x-small`, `small`, `medium`, `large`, `x-large`, `xx-large`) and a couple of _relative_ keyword values (`smaller`, `larger`). The relative values are relative to the parent element's `font-size`.

  CodePen Embed - Text | font-size keywords v2  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

  CodePen Embed - Text | font-size v4  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Change the space between lines

Use [`line-height`](https://developer.mozilla.org/docs/Web/CSS/line-height) to specify the height of each line in an element. This property accepts either a number, length, percentage, or the keyword `normal`. Generally, it's recommended to use a number instead of a length or percentage to avoid issues with inheritance.

  CodePen Embed - Text | line-height  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

  CodePen Embed - Text | line-height inheritance issue v6 (show selectors)  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Change the space between characters

Use [`letter-spacing`](https://developer.mozilla.org/docs/Web/CSS/letter-spacing) to control the amount of horizontal space between characters in your text. This property accepts length values such as `em`, `px`, and `rem`.

Note that the specified value _increases_ the amount of natural space between characters. In the following demo, try selecting an individual letter to see the size of its letterbox and how it changes with `letter-spacing`.

  CodePen Embed - Text | letter-spacing (static)  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Change the space between words

Use [`word-spacing`](https://developer.mozilla.org/docs/Web/CSS/word-spacing) to increase or decrease the length of space between each word in your text. This property accepts length values such as `em`, `px`, and `rem`. Note that the length you specify is for _extra_ space in addition to the normal spacing. This means that `word-spacing: 0` is equivalent to `word-spacing: normal`.

  CodePen Embed - Text | word-spacing (slider, relative val)  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## `font` shorthand

You can use the shorthand [`font`](https://developer.mozilla.org/docs/Web/CSS/font) property to set many font-related properties at once. The list of possible properties are [`font-family`](#change_the_typeface), [`font-size`](#change_the_size_of_text), [`font-stretch`](https://developer.mozilla.org/docs/Web/CSS/font-stretch), [`font-style`](#use_italic_and_oblique_fonts), [`font-variant`](#font-variant), [`font-weight`](#make_text_bold), and [`line-height`](#change_the_space_between_lines).

Check out [MDN's `font` article](https://developer.mozilla.org/docs/Web/CSS/font#syntax) for the specifics of how to order these properties.

  CodePen Embed - Text | font shorthand  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Change the case of text

Use [`text-transform`](https://developer.mozilla.org/docs/Web/CSS/text-transform) to modify the capitalization of your text without needing to change the underlying HTML. This property accepts the following keyword values: `uppercase`, `lowercase`, and `capitalize`.

  CodePen Embed - Text | text-transform  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Add underlines, overlines, and through-lines to text

Use [`text-decoration`](https://developer.mozilla.org/docs/Web/CSS/text-decoration) to add lines to your text. Underlines are most commonly used, but it's possible to add lines above your text or right through it!

The `text-decoration` property is shorthand for the more specific properties detailed below.

The [`text-decoration-line`](https://developer.mozilla.org/docs/Web/CSS/text-decoration-line) property accepts the keywords `underline`, `overline`, and `line-through`. You can also specify multiple keywords for multiple lines.

  CodePen Embed - Text | text-decoration-line  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

The [`text-decoration-color`](https://developer.mozilla.org/docs/Web/CSS/text-decoration-color) property sets the color of all decorations from `text-decoration-line`.

  CodePen Embed - Text | text-decoration-color  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

The [`text-decoration-style`](https://developer.mozilla.org/docs/Web/CSS/text-decoration-style) property accepts the keywords `solid`, `double`, `dotted`, `dashed`, and `wavy`.

  CodePen Embed - Text | text-decoration-style  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

The [`text-decoration-thickness`](https://developer.mozilla.org/docs/Web/CSS/text-decoration-thickness) property accepts any length values and sets the stroke width of all decorations from `text-decoration-line`.

  CodePen Embed - Text | text-decoration-thickness  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

The `text-decoration` property is a shorthand for all the above properties.

  CodePen Embed - Text | text-decoration  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Add an indent to your text

Use [`text-indent`](https://developer.mozilla.org/docs/Web/CSS/text-indent) to add an indent to your blocks of text. This property takes either a length (for example, `10px`, `2em`) or a percentage of the containing block's width.

  CodePen Embed - Text | text-indent (slider)  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Deal with overflowing or hidden content

Use [`text-overflow`](https://developer.mozilla.org/docs/Web/CSS/text-overflow) to specify how hidden content is represented. There are two options: `clip` (the default), which truncates the text at the point of overflow; and `ellipsis`, which displays an ellipsis (…) at the point of overflow.

  CodePen Embed - Text | text-overflow  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Control white-space

The [`white-space`](https://developer.mozilla.org/docs/Web/CSS/white-space) property is used to specify how whitespace in an element should be handled. For more details, check out the [`white-space` article on MDN](https://developer.mozilla.org/docs/Web/CSS/white-space).

  CodePen Embed - Text | white-space  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

`white-space: pre` can be useful for rendering [ASCII art](https://en.wikipedia.org/wiki/ASCII_art) or carefully indented code blocks.

  CodePen Embed - Text | white-space 2  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Control how words break

Use [`word-break`](https://developer.mozilla.org/docs/Web/CSS/word-break) to change how words should be "broken" when they would overflow the line. By default, the browser won't split words. Using the keyword value `break-all` for `word-break` will instruct the browser to break words at individual characters if necessary.

  CodePen Embed - Text | word-break (with labels) (slider)  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Change text alignment

Use [`text-align`](https://developer.mozilla.org/docs/Web/CSS/text-align) to specify the horizontal alignment of text in a block or table-cell element. This property accepts the keyword values `left`, `right`, `start`, `end`, `center`, `justify`, and `match-parent`.

The values `left` and `right` align the text to the left and right sides of the block, respectively.

Use `start` and `end` to represent the location of the start and end of a line of text in the current writing mode. Therefore, `start` maps to `left` in English, and to `right` in Arabic script which is written right to left (RTL). They're logical alignments, learn more in our [logical properties](https://web.dev/learn/css/logical-properties) module.

Use `center` to align the text to the center of the block.

The value of `justify` organizes the text and changes word spacings automatically so that the text lines up with both the left and right edges of the block.

  CodePen Embed - Text | text-align  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Change the direction of text

Use [`direction`](https://developer.mozilla.org/docs/Web/CSS/direction) to set the direction of your text, either `ltr` (left to right, the default) or `rtl` (right to left). Some languages like Arabic, Hebrew, or Persian are written right to left, so `direction: rtl` should be used. For English and all other left-to-right languages, use `direction: ltr`.

## Change the flow of text

Use [`writing-mode`](https://developer.mozilla.org/docs/Web/CSS/writing-mode) to change the way text flows and is arranged. The default is `horizontal-tb`, but you can also set `writing-mode` to `vertical-lr` or `vertical-rl` for text that you want to flow horizontally.

  CodePen Embed - Text | writing-mode v2  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Change the orientation of text

Use [`text-orientation`](https://developer.mozilla.org/docs/Web/CSS/text-orientation) to specify the orientation of characters in your text. The valid values for this property are `mixed` and `upright`. This property is only relevant when [`writing-mode`](#change_the_flow_of_text) is set to something other than `horizontal-tb`.

  CodePen Embed - Text | text-orientation  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Add a shadow to text

Use [`text-shadow`](https://developer.mozilla.org/docs/Web/CSS/text-shadow) to add a shadow to your text. This property expects three lengths (`x-offset`, `y-offset`, and `blur-radius`) and a color.

  CodePen Embed - Text | text-shadow  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Check out [the `text-shadow` section of our module on Shadows](https://web.dev/learn/css/shadows#text_shadow) to learn more.

## Variable fonts

Typically, "normal" fonts require importing different files for different versions of the typeface, like bold, italic, or condensed. Variable fonts are fonts that can contain many different variants of a typeface in one file.

Roboto Flex in random combinations of Width and Weight

Check out [our article on Variable Fonts](https://web.dev/articles/variable-fonts) for more details.

## Pseudo-elements

## `::first-letter` and `::first-line` pseudo-elements

The [`::first-letter`](https://developer.mozilla.org/docs/Web/CSS/::first-letter) and [`::first-line`](https://developer.mozilla.org/docs/Web/CSS/::first-line) pseudo-elements target a text element's first letter and first line respectively.

  CodePen Embed - Text | ::first-line & ::first-letter  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## `::selection` pseudo-element

Use the [`::selection`](https://developer.mozilla.org/docs/Web/CSS/::selection) pseudo-element to change the appearance of user-selected text.

When using this pseudo-element, only certain CSS properties can be used: `color`, `background-color`, `text-decoration`, `text-shadow`, `stroke-color`, `fill-color`, `stroke-width`.

  CodePen Embed - Text | ::selection  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## font-variant

The [`font-variant`](https://developer.mozilla.org/docs/Web/CSS/font-variant) property is a shorthand for a number of CSS properties that let you choose font variants like `small-caps` and `slashed-zero`. The CSS properties this shorthand includes are [`font-variant-alternates`](https://developer.mozilla.org/docs/Web/CSS/font-variant-alternates), [`font-variant-caps`](https://developer.mozilla.org/docs/Web/CSS/font-variant-caps), [`font-variant-east-asian`](https://developer.mozilla.org/docs/Web/CSS/font-variant-east-asian), [`font-variant-ligatures`](https://developer.mozilla.org/docs/Web/CSS/font-variant-ligatures), and [`font-variant-numeric`](https://developer.mozilla.org/docs/Web/CSS/font-variant-numeric). Check out the links on each property for more details about its usage.

  CodePen Embed - Text | font-variant shorthand  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Check your understanding

Test your knowledge of typography on the web

Which of the following keywords can be used as a `font-family` generic fallback?

Which statement is used to convert the first letter of each word to uppercase? e.g. `This is a sentence.` ➡ `This Is A Sentence.`

`font-variant: capitalize;`

`text-transform: capitalize;`

True or False: Use `text-orientation` to align text to the left, right, or center.

Which CSS property can be used to change the space between lines of text?

## Resources

*   [Font best practices](https://web.dev/articles/font-best-practices) discusses importing fonts, rendering fonts, and other best practices for using fonts on the web.
*   [MDN Fundamental text and font styling](https://developer.mozilla.org/docs/Learn/CSS/Styling_text/Fundamentals).

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
