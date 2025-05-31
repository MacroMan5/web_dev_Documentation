# Media queries  |  web.dev

**Source URL:** [https://web.dev/learn/design/media-queries?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%2Fmedia-queries](https://web.dev/learn/design/media-queries?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%2Fmedia-queries)  
**Last Updated:** 2025-05-23T00:54:11.354Z  
**Extracted:** 2025-05-31 16:58:10

---

# Media queries  |  web.dev

Designers can adjust their designs to accommodate users. The clearest example of this is the form factor of a user's device; its width, the device aspect ratio, and so on. Using media queries, designers can respond to these different form factors.

Media queries are initiated with the `@media` keyword (a CSS at-rule), and can be used for a variety of use cases.

## Target different types of output

Websites are often displayed on screens but CSS can also be used to style websites for other outputs too. You might want your web pages to look one way on a screen but different when printed out. Querying media types makes this possible.

In this example, the background color is set to grey. But if the page is printed, the background color should be transparent. This saves the user's printer ink.

```
body {
  color: black;
  background-color: grey;
}

@media print {
  body {
    background-color: transparent;
  }
}
```

You can use the `@media` at-rule in your stylesheet like that, or you can make a separate stylesheet and use the `media` attribute on a `link` element:

```
<link rel="stylesheet" href="global.css">
<link rel="stylesheet" href="print.css" media="print">
```

If you don't specify any media type for your CSS, it will automatically have a media type value of `all`. These two blocks of CSS are equivalent:

```
body {
  color: black;
  background-color: white;
}
```
```
@media all {
   body {
     color: black;
     background-color: white;
   }
}
```

These two lines of HTML are also equivalent:

```
<link rel="stylesheet" href="global.css">
```
```
<link rel="stylesheet" href="global.css" media="all">
```

### Query conditions

You can add conditions to media types. These are called media queries. The CSS is applied only if the media type matches and the condition is also true. These conditions are called _media features_.

This is the syntax for media queries:

```
@media type and (feature)
```

You can use media queries on a `link` element if your styles are in a separate stylesheet:

```
<link rel="stylesheet" href="specific.css" media="type and (feature)">
```

Let's say you want to apply different styles depending on whether the browser window is in landscape mode (the viewport width is greater than its height) or portrait mode (the viewport height is greater than its width). There's a media feature called `orientation` you can use to test that:

```
@media all and (orientation: landscape) {
   // Styles for landscape mode.
}
@media all and (orientation: portrait) {
   // Styles for portrait mode.
}
```

Or if you prefer to have separate stylesheets:

```
<link rel="stylesheet" href="landscape.css" media="all and (orientation: landscape)">
<link rel="stylesheet" href="portrait.css" media="all and (orientation: portrait)">
```

In this case the media type is `all`. Because that's the default value, you can leave it out if you want:

```
@media (orientation: landscape) {
   // Styles for landscape mode.
}
@media (orientation: portrait) {
   // Styles for portrait mode.
}
```

Or using separate stylesheets:

```
<link rel="stylesheet" href="landscape.css" media="(orientation: landscape)">
<link rel="stylesheet" href="portrait.css" media="(orientation: portrait)">
```

  CodePen Embed - Orientation media query  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

While using separate stylesheets for different media _types_—like `print`—might be okay, it's probably not a good idea to use a separate stylesheet for every media _query_. Use `@media` at-rules instead.

## Adjust styles based on viewport size

For responsive design, one of the most useful media features involves the dimensions of the browser viewport. To apply styles when the browser window is wider than a certain width, use `min-width`.

```
@media (min-width: 400px) {
  // Styles for viewports wider than 400 pixels.
}
```

Use the `max-width` media feature to apply styles below a certain width:

```
@media (max-width: 400px) {
  // Styles for viewports narrower than 400 pixels.
}
```

You can use any CSS [length units](https://developer.mozilla.org/docs/Web/CSS/length) in your media queries. If your content is mostly image-based, pixels might make the most sense. If your content is mostly text-based, it probably makes more sense to use a [relative unit](https://web.dev/learn/css/sizing#relative_lengths) that's based on text size, like `em` or `ch`:

```
@media (min-width: 25em) {
  // Styles for viewports wider than 25em.
}
```

You can also combine media queries to apply more than one condition. Use the word `and` to combine your media queries:

```
@media (min-width: 50em) and (max-width: 60em) {
  // Styles for viewports wider than 50em and narrower than 60em.
}
```

  CodePen Embed - LearnDesign: Combining media queries  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Choose breakpoints based on the content

The point at which a media feature condition becomes true is called a breakpoint. It's best to choose your breakpoints based on your content rather than popular device sizes, as those are subject to change with every technology release cycle.

In this example, `50em` is the point at which the lines of text become uncomfortably long. So a breakpoint is created to make the interface more legible. Using the `column-count` property, the text is divided into two columns from that point on.

```
@media (min-width: 50em) {
  article {
    column-count: 2;
  }
}
```

  CodePen Embed - LearnDesign: Horizontal media query  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Combinations

You can use media queries based on the height of the viewport, not just the width. This could be useful for optimizing interface content "above the fold". In the previous example, if readers are using a wide but short browser window, they have to scroll down one column and then scroll back up to get to the top of the second column. It would be safer to only apply the columns when the viewport is both wide enough and tall enough.

You can combine media queries so that the styles only apply when all the conditions are true. In this example, the viewport must be at least `50em` wide and `30em` tall in order for the column styles to be applied. Those breakpoints were chosen based on the amount of content.

```
@media (min-width: 50em) and (min-height: 30em) {
  article {
    column-count: 2;
  }
}
```

  CodePen Embed - LearnDesign: Horizontal and vertical media queries  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

These examples show how media queries can be used to adapt designs to the form factor of a user's device, but these just scratch the surface of possibilities. Media queries can go far beyond width and height, accessing user preferences for accessibility features and theme colors. Using media queries to make layout adjustments is a great start to a responsive design, which builds on these features and more.

### Check your understanding

Test your knowledge of responsive media queries.

Media queries only exist for screen size?

Screens are the only place web content is consumed or displayed?

The default media type is?

What would you use to prevent the browser from scaling a design on mobile?

`<meta name="viewport" content="width=device-width, initial-scale=1">`

Which media query applies when the browser window is _above_ `720px`.

`@media (min-width: 720px)`

`@media (clamp-width: 720px)`

`@media (max-width: 720px)`

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
