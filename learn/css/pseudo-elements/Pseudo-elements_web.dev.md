# Pseudo-elements  |  web.dev

**Source URL:** [https://web.dev/learn/css/pseudo-elements?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Fpseudo-elements](https://web.dev/learn/css/pseudo-elements?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Fpseudo-elements)  
**Last Updated:** 2025-05-23T01:09:39.646Z  
**Extracted:** 2025-05-31 16:58:10

---

# Pseudo-elements  |  web.dev

Pseudo-elements

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

##### [The CSS Podcast - 014: Pseudo-elements](https://thecsspodcast.libsyn.com/014-pseudo-elements)

If you've got an article of content and you want the first letter to be a much bigger drop cap— how do you achieve that?

![A couple of paragraphs of text with a blue drop cap](https://web.dev/static/learn/css/pseudo-elements/image/a-couple-paragraphs-tex-c9d26a842603e.svg)

In CSS, you can use the `::first-letter` pseudo-element to achieve this sort of design detail.

```
p::first-letter {
  color: blue;
  float: left;
  font-size: 2.6em;
  font-weight: bold;
  line-height: 1;
  margin-inline-end: 0.2rem;
}
```

  CodePen Embed - Learn CSS - Drop cap  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

A pseudo-element is like adding or targeting an extra element without having to add more HTML. This example solution, using `::first-letter`, is one of many pseudo-elements. They have a range of roles, and in this lesson you're going to learn which pseudo-elements are available and how you can use them.

## `::before` and `::after`

Both the [`::before`](https://developer.mozilla.org/docs/Web/CSS/::before) and [`::after`](https://developer.mozilla.org/docs/Web/CSS/::after) pseudo-elements create a child element inside an element **only** if you define a `content` property.

```
.my-element::before {
    content: "";
}

.my-element::after {
    content: "";
}
```

The `content` can be any string —even an empty one— but be mindful that anything other than an empty string will likely be announced by a screen reader. You can add an image `url`, which will insert an image at its original dimensions, so you won't be able to resize it. You can also insert a [`counter`](https://developer.mozilla.org/docs/Web/CSS/counter\(\)).

Once a `::before` or `::after` element has been created, you can style it however you want with no limits. You can only insert a `::before` or `::after` element to an element that will accept child elements ([elements with a document tree](https://www.w3.org/TR/CSS21/generate.html)), so elements such as `<img />`, `<video>` and `<input>` won't work.

  CodePen Embed - Learn CSS - Callout  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## `::first-letter`

We met this pseudo-element at the start of the lesson. It is worth being aware that not all CSS properties can be used when targeting [`::first-letter`](https://developer.mozilla.org/docs/Web/CSS/::first-letter). The available properties are:

*   `color`
*   `background` properties (such as `background-image`)
*   `border` properties (such as `border-color`)
*   `float`
*   `font` properties (such as `font-size` and `font-weight`)
*   text properties (such as `text-decoration` and `word-spacing`)

```
p::first-letter {
  color: goldenrod;
  font-weight: bold;
}
```

  CodePen Embed - Learn CSS - First letter  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## `::first-line`

The [`::first-line`](https://developer.mozilla.org/docs/Web/CSS/::first-line) pseudo-element will let you style the first line of text only if the element with `::first-line` applied has a `display` value of `block`, `inline-block`, `list-item`, `table-caption` or `table-cell`.

```
p::first-line {
  color: goldenrod;
  font-weight: bold;
}
```

  CodePen Embed - Learn CSS - First line  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Like the `::first-letter` pseudo-element, there's only a subset of CSS properties you can use:

*   `color`
*   `background` properties
*   `font` properties
*   `text` properties

## `::backdrop`

If you have an element that is presented in full screen mode, such as a `<dialog>` or a `<video>`, you can style the backdrop—the space between the element and the rest of the page—with the [`::backdrop`](https://developer.mozilla.org/docs/Web/CSS/::backdrop) pseudo-element:

```
video::backdrop {
  background-color: goldenrod;
}
```

  CodePen Embed - Learn CSS - The ::backdrop pseudo-element  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## `::marker`

The [`::marker`](https://developer.mozilla.org/docs/Web/CSS/::marker) pseudo-element lets you style the bullet or number for a list item or the arrow of a `<summary>` element.

```
::marker {
  color: hotpink;
}

ul ::marker {
  font-size: 1.5em;
}

ol ::marker {
  font-size: 1.1em;
}

summary::marker {
  content: '\002B'' '; /* Plus symbol with space */
}

details[open] summary::marker {
  content: '\2212'' '; /* Minus symbol with space */
}
```

Only a small subset of CSS properties are supported for `::marker`:

*   `color`
*   `content`
*   `white-space`
*   `font` properties
*   `animation` and `transition` properties

You can change the marker symbol, using the `content` property. You can use this to set a plus and minus symbol for the closed and empty states of a `<summary>` element, for example.

  CodePen Embed - Learn CSS - The ::marker pseudo-element  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## `::selection`

The [`::selection`](https://developer.mozilla.org/docs/Web/CSS/::selection) pseudo-element allows you to style how selected text looks.

```
::selection {
  background: green;
  color: white;
}
```

  CodePen Embed - Learn CSS - Global selection style  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

This pseudo-element can be used to style all selected text as in the above demo. It can also be used in combination with other selectors for a more specific selection style.

```
p:nth-of-type(2)::selection {
  background: darkblue;
  color: yellow;
}
```

  CodePen Embed - Learn CSS - Specific selection style  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

As with other pseudo-elements, only a subset of CSS properties are allowed:

*   `color`
*   `background-color` but **not** `background-image`
*   `text` properties

## `::placeholder`

You can add a helper hint to form elements, such as `<input>` with a `placeholder` attribute. The [`::placeholder`](https://developer.mozilla.org/docs/Web/CSS/::placeholder) pseudo-element allows you to style that text.

```
input::placeholder {
  color: darkcyan;
}
```

  CodePen Embed - Learn CSS - Input with placeholder style  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

The `::placeholder` only supports a subset of CSS rules:

*   `color`
*   `background` properties
*   `font` properties
*   `text` properties

## `::cue`

Last in this tour of pseudo-elements is the [`::cue`](https://developer.mozilla.org/docs/Web/CSS/::cue) pseudo-element. This allows you to style the WebVTT cues, which are the captions of a `<video>` element.

You can also pass a selector into a `::cue`, which allows you to style specific elements _inside_ a caption.

```
video::cue {
  color: yellow;
}

video::cue(b) {
  color: red;
}

video::cue(i) {
  color: lightpink;
}
```

### Check your understanding

Test your knowledge of pseudo-elements

Which of the following are not pseudo-elements?

Pseudo-elements can be found in an HTML file.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
