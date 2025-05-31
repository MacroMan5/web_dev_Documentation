# Sizing Units  |  web.dev

**Source URL:** [https://web.dev/learn/css/sizing?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Fsizing](https://web.dev/learn/css/sizing?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Fsizing)  
**Last Updated:** 2025-05-23T01:06:55.443Z  
**Extracted:** 2025-05-31 16:58:10

---

# Sizing Units  |  web.dev

##### [The CSS Podcast - 008: Sizing Units](https://thecsspodcast.libsyn.com/tcp-css-podcast-episode-008)

The web is a responsive medium, but sometimes you want to control its dimensions to improve the overall interface quality. A good example of this is limiting line lengths to improve readability. How would you do that in a flexible medium like the web?

  CodePen Embed - Learn CSS - Units - Intro  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

For this case, you can use a `ch` unit, which is equal to the width of a "0" character in the rendered font at its computed size. This unit allows you to limit the width of text with a unit that's designed to size text, which in turn, allows predictable control regardless of the size of that text. The `ch` unit is one of a handful of units that are helpful for specific contexts like this example.

## Numbers

Numbers are used to define `opacity`, `line-height` and even for color channel values in `rgb`. Numbers are unitless integers (1, 2, 3, 100) and decimals (.1, .2, .3).

Numbers have meaning depending on their context. For example, when defining `line-height`, a number is representative of a ratio if you define it without a supporting unit:

```
p {
  font-size: 24px;
  line-height: 1.5;
}
```

  CodePen Embed - Learn CSS - Sizing - Numbers  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

In this example, `1.5` is equal to **150%** of the `p` element's **computed pixel font size**. This means that if the `p` has a `font-size` of `24px`, the line height will be computed as `36px`.

Numbers can also be used in the following places:

*   When setting values for filters: `filter: sepia(0.5)` applies a `50%` sepia filter to the element.
*   When setting opacity: `opacity: 0.5` applies a `50%` opacity.
*   In color channels: `rgb(50, 50, 50)`, where the values 0-255 are acceptable to set a color value. [See color lesson](https://web.dev/learn/css/color).
*   To transform an element: `transform: scale(1.2)` scales the element by 120% of its initial size.

## Percentages

When using a percentage in CSS you need to know how the percentage is calculated. For example,`width` is calculated as a percentage of the available width in the parent element.

```
div {
  width: 300px;
  height: 100px;
}

div p {
  width: 50%; 
}
```

  CodePen Embed - Learn CSS - Sizing - Percentages  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

In the above example, the width of `div p` is `150px`, assuming that the layout uses the default `box-sizing: content-box`.

If you set `margin` or `padding` as a percentage, they will be a portion of the **parent element's width**, regardless of direction.

```
div {
  width: 300px;
  height: 100px;
}

div p {
  margin-top: 50%; /* calculated: 150px */
  padding-left: 50%; /* calculated: 150px */
}
```

  CodePen Embed - Learn CSS - Sizing - Percentages 2  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

In the above snippet, both the `margin-top` and `padding-left` will compute to `150px`.

```
div {
  width: 300px;
  height: 100px;
}

div p {
  width: 50%; /* calculated: 150px */
  transform: translateX(10%); /* calculated: 15px */
}
```

  CodePen Embed - Learn CSS - Sizing - Percentages 3  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

If you set a `transform` value as a percentage, it is based on the element with the transform set. In this example, the `p` has a `translateX` value of `10%` and a `width` of `50%`. First, calculate what the width will be: `150px` because it is **50% of its parent's width**. Then, take `10%` of `150px`, which is `15px`.

## Dimensions and lengths

If you attach a unit to a number, it becomes a dimension. For example, `1rem` is a dimension. In this context, the unit that is attached to a number is referred to in specifications as a dimension token. Lengths are **dimensions that refer to distance** and they can either be absolute or relative.

### Absolute lengths

All absolute lengths resolve against the same base, making them predictable wherever they're used in your CSS. For example, if you use `cm` to size your element and then print, it should be accurate if you compared it to a ruler.

```
div {
  width: 10cm;
  height: 5cm;
  background: black;
}
```

If you printed this page, the `div` would print as a 10x5cm black rectangle. Keep in mind, CSS is used not only for digital content, but also to style print content. Absolute lengths can really come in handy when designing for print.

| Unit | Name | Equivalent to |
| --- | --- | --- |
| [cm](https://www.w3.org/TR/css-values-4/#cm) | Centimeters | 1cm = 96px/2.54 |
| [mm](https://www.w3.org/TR/css-values-4/#mm) | Millimeters | 1mm = 1/10th of 1cm |
| [Q](https://www.w3.org/TR/css-values-4/#q) | Quarter-millimeters | 1Q = 1/40th of 1cm |
| [in](https://www.w3.org/TR/css-values-4/#in) | Inches | 1in = 2.54cm = 96px |
| [pc](https://www.w3.org/TR/css-values-4/#pc) | Picas | 1pc = 1/6th of 1in |
| [pt](https://www.w3.org/TR/css-values-4/#pt) | Points | 1pt = 1/72th of 1in |
| [px](https://www.w3.org/TR/css-values-4/#px) | Pixels | 1px = 1/96th of 1in |

### Relative lengths

A relative length is calculated against a base value, much like a percentage. The difference between these and percentages is that you can contextually size elements. This means that CSS has units such as `ch` that use the text size as a basis, and `vw` which is based on the width of the viewport (your browser window). Relative lengths are particularly useful on the web due to its responsive nature.

#### Font-size-relative units

CSS provides helpful units that are relative to the size of elements of rendered typography, such as the size of the text itself (`em` units) or width of the typefaces characters (`ch` units).

| unit | relative to: |
| --- | --- |
| [em](https://www.w3.org/TR/css-values-4/#em) | Relative to the font size, i.e. 1.5em will be 50% larger than the base computed font size of its parent. (Historically, the height of the capital letter "M"). |
| [ex](https://www.w3.org/TR/css-values-4/#ex) | Heuristic to determine whether to use the x-height, a letter "x", or \`.5em\` in the current computed font size of the element. |
| [cap](https://www.w3.org/TR/css-values-4/#cap) | Height of the capital letters in the current computed font size of the element. |
| [ch](https://www.w3.org/TR/css-values-4/#ch) | Average [character advance](https://www.w3.org/TR/css-values-4/#length-advance-measure) of a narrow glyph in the element's font (represented by the "0" glyph). |
| [ic](https://www.w3.org/TR/css-values-4/#ic) | Average [character advance](https://www.w3.org/TR/css-values-4/#length-advance-measure) of a full width glyph in the element's font, as represented by the "水" (CJK water ideograph, U+6C34) glyph. |
| [rem](https://www.w3.org/TR/css-values-4/#rem) | Font size of the root element (default is 16px). |
| [lh](https://www.w3.org/TR/css-values-4/#lh) | Line height of the element. |
| [rlh](https://www.w3.org/TR/css-values-4/#rlh) | Line height of the root element. |

![The text, CSS is 10x great with labels for ascender height, descender height and x-height. The x-height represents 1ex and the 0 represents 1ch](https://web.dev/static/learn/css/sizing/image/the-text-css-is-10x-grea-54e1b11dfc1ef.svg)

#### Viewport-relative units

You can use the dimensions of the viewport (browser window) as a relative basis. These units portion up the available viewport space.

| unit | relative to |
| --- | --- |
| [vw](https://www.w3.org/TR/css-values-4/#vw) | 1% of viewport's width. People use this unit to do cool font tricks, like resizing a header font based on the width of the page so as the user resizes, the font will also resize. |
| [vh](https://www.w3.org/TR/css-values-4/#vh) | 1% of viewport's height. You can use this to arrange items in a UI, if you have a footer toolbar for example. |
| [vi](https://www.w3.org/TR/css-values-4/#vi) | 1% of viewport's size in the root element's [inline axis](https://www.w3.org/TR/css-writing-modes-4/#inline-axis). Axis refers to writing modes. In horizontal writing modes like English, the inline axis is horizontal. In vertical writing modes like some Japanese typefaces, the inline axis runs top to bottom. |
| [vb](https://www.w3.org/TR/css-values-4/#vb) | 1% of viewport's size in the root element's [block axis](https://www.w3.org/TR/css-writing-modes-4/#block-axis). For the block axis, this would be the directionality of the language. LTR languages like English would have a vertical block axis, since English language readers parse the page from top to bottom. A vertical writing mode has a horizontal block axis. |
| [vmin](https://www.w3.org/TR/css-values-4/#vmin) | 1% of the viewport's smaller dimension. |
| [vmax](https://www.w3.org/TR/css-values-4/#vmax) | 1% of the viewport's larger dimension. |

```
div {
  width: 10vw;
}

p {
  max-width: 60ch;
}
```

  CodePen Embed - Learn CSS - Sizing - Relative Units  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

In this example, the `div` will be 10% of the viewport's width because `1vw` is **1% of the viewport width**. The `p` element has a `max-width` of `60ch` which means it can't exceed the width of 60 "0" characters in the calculated font and size.

## Miscellaneous units

There are some other units which have been specified to deal with particular types of values.

### Angle units

In the [color module](https://web.dev/learn/css/color), we looked at **angle units**, which are helpful for defining degree values, such as the hue in `hsl`. They are also useful for rotating elements within transform functions.

```
div {
  width: 150px;
  height: 150px;
  transform: rotate(60deg);
}
```

  CodePen Embed - Learn CSS - Sizing - Misc Units  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Using the `deg` angle unit, you can rotate a `div` 90° on its center axis.

```
div {
  background-image: url('a-low-resolution-image.jpg');
}

@media (-webkit-min-device-pixel-ratio: 2), (min-resolution: 192dpi) {
  div {
    background-image: url('a-high-resolution-image.jpg');
  }
}
```

#### Resolution units

In the previous example the value of `min-resolution` is `192dpi`. The `dpi` unit stands for **dots per inch**. A useful context for this is detecting very high resolution screens, such as Retina displays in a media query and serving up a higher resolution image.

### Check your understanding

Test your knowledge of sizing

Which of the following are valid dimensions?

How are absolute and relative units different?

An absolute length is calculated against a single shared base value, where a relative unit is compared against a base value that can change.

Absolute values can't change but relative units can

Viewport units are absolute.

## Resources

*   [CSS Spec Values and Units Level 4](https://www.w3.org/TR/css-values-4)
*   [Sizing and Units on MDN](https://developer.mozilla.org/docs/Learn/CSS/Building_blocks/Values_and_units)
*   [All About Ems](https://learn.scannerlicker.net/2014/07/31/so-how-much-is-an-em/)
*   [A percentages explainer](https://wattenberger.com/blog/css-percents)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
