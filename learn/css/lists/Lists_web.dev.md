# Lists  |  web.dev

**Source URL:** [https://web.dev/learn/css/lists?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Flists](https://web.dev/learn/css/lists?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Flists)  
**Last Updated:** 2025-05-23T01:06:56.157Z  
**Extracted:** 2025-05-31 16:58:10

---

# Lists  |  web.dev

##### [The CSS Podcast - 030: Lists](https://thecsspodcast.libsyn.com/030-lists)

Imagine you have a bunch of items you plan to buy during your next grocery trip. One common way to represent this visually is a list—but how can you add styling to your grocery list?

```
<ul>
  <li>oat milk</li>
  <li>rhubarb</li>
  <li>cereal</li>
  <li>pie crust</li>
</ul>
```

  CodePen Embed - Learn CSS: Lists - Basic List  

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

## Creating a List

The preceding list started with a semantic element, or `<ul>`, with grocery list items (`<li>` elements) as children. If you inspect each `<li>` element you can see that they all have `display: list-item`, which is why the browser renders a `::marker` by default.

```
li {
  display: list-item;
}
```

There are two other types of lists.

Ordered lists can be created with `<ol>`, in which case the list-item will display a number as the `::marker`.

```
<ol>
  <li>oat milk</li>
  <li>rhubarb</li>
  <li>cereal</li>
  <li>pie crust</li>
</ol>
```

And description lists are created with `<dl>`, however this list type does not use the `<li>` list item element.

```
<dl>
  <dt>oat milk</dt>
  <dd>- non dairy trendy drink</dd>
  <dt>cereal</dt>
  <dd>- breakfast food</dd>
</dl>
```

  CodePen Embed - Learn CSS: Lists - Types of Lists  

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## List styles

Now that you know how to make a list, you can style them. The first CSS properties to discover are those that are applied to the entire list.

There are three list-style properties you can use to style your example: `list-style-position`, `list-style-image`, and `list-style-type`.

### `list-style-position`

[`list-style-position`](https://developer.mozilla.org/docs/Web/CSS/list-style-position) allows you to move your bullet point to either `inside` or `outside` the list-item's contents. The default `outside` means the bullet point is not included in the list items contents while `inside` moves the first element among the list item's contents.

![A list with both outside and inside ::marker which shows that outside (default value) is not in the list-item and is inside the list-item content box.](https://web.dev/static/learn/css/lists/image/a-list-both-outside-ins-cc3285c12d7cc.jpg)

  CodePen Embed - Learn CSS: Lists - list-style-position  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### `list-style-image`

[`list-style-image`](https://developer.mozilla.org/docs/Web/CSS/list-style-image) allows you to replace your list's bullet points with images. This enables you to set an image such as an `url` or `none` to make your bullets an image, svg or gif even. You can also use any media type or even a data URI.

Let's look at how we can add an image of each of our grocery items as the `list-style-image`:

  CodePen Embed - Learn CSS: Lists - list-style-image  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### `list-style-type`

The final option is to style the [`list-style-type`](https://developer.mozilla.org/docs/Web/CSS/list-style-type) which changes the bullet points to known style keywords, custom strings, emoji and more. You can view all of the possible list style types [here](https://developer.mozilla.org/docs/Web/CSS/list-style-type).

  CodePen Embed - Learn CSS: Lists - list-style-type  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### `list-style` shorthand

Now that you have all of these individual properties, you can use the [`list-style`](https://developer.mozilla.org/docs/Web/CSS/list-style) shorthand to set all of our list styles in one line:

```
list-style: <'list-style-type'> || <'list-style-position'> || <'list-style-image'>
```

`list-style` allows you to declare combinations of one, two, or three of the `list-style` properties in any order. If `list-style-type` and `list-style-image` are both set, then`list-style-type` is used as a fallback if the image is unavailable.

```
/* type */
list-style: square;

/* image */
list-style: url('../img/shape.png');

/* position */
list-style: inside;

/* type | position */
list-style: georgian inside;

/* type | image | position */
list-style: lower-roman url('../img/shape.png') outside;

/* Keyword value */
list-style: none;

/* Global values */
list-style: inherit;
list-style: initial;
list-style: revert;
list-style: unset;
```

This is the most commonly used property of the list styles covered in this section. One common application is `list-style: none` to hide default styles. Default styles come from the browser, and you often see reset stylesheets removing list styles like padding and margins. You can also use this shorthand to set styles, like `list-style: square inside;`

  CodePen Embed - Learn CSS: Lists - list-style playground  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

So far, the examples have focused on styling an entire list and list items, but what about a more granular approach?

## `::marker` pseudo-element

The `list-item` marker element is the bullet, hyphen, or roman numeral that helps indicate each item in your list.

![A list with three items which shows that each of the bullets are ::marker pseudo-elements.](https://web.dev/static/learn/css/lists/image/a-list-three-items-show-bcda4715c5de5.jpg)

If you inspect the list in DevTools, you can see a `::marker` element for each of the list items, despite not declaring any in HTML. If you inspect the `::marker` further, you'll see the browser default styling for it.

```
::marker {
    unicode-bidi: isolate;
    font-variant-numeric: tabular-nums;
    text-transform: none;
    text-indent: 0px !important;
    text-align: start !important;
    text-align-last: start !important;
}
```

When you declare a list, each item is given a marker, despite there being no bullet point or roman numeral in your HTML. This is a pseudo-element because the browser generates it for you, and provides a limited styling API to target it. [Learn more about the anatomy of the CSS bullet.](https://web.dev/articles/css-marker-pseudo-element) `::marker` has [limited support](https://developer.mozilla.org/docs/Web/CSS/::marker#browser_compatibility) in Safari.

### Marker box

In the CSS layout model, list item markers are represented by a marker box associated with each list item. The marker box is the container which typically contains the bullet or number.

To style the marker box, you can use the `::marker` selector. This allows you to select just the marker instead of styling based on the entire list.

  CodePen Embed - Learn CSS: Lists - ::marker intro  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Marker styles

Now that you have selected the marker, let's look at the styling properties available to this selector. You can learn more about [Custom bullets with CSS ::marker](https://web.dev/articles/css-marker-pseudo-element) on web.dev.

There are quite a few allowed CSS `::marker` Properties:

*   `animation-*`
*   `transition-*`
*   `color`
*   `direction`
*   `font-*`
*   `content`
*   `unicode-bidi`
*   `white-space`

  CodePen Embed - Learn CSS: Lists - ::marker playground  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Display type

All of our `list-style` and `::marker` properties know to style `<li>` elements because they have a default display value of list-item. You can also make things that aren't an `<li>` into a list item.

You do this by adding the property `display: list-item`. One example of using `display: list-item` is if you want a hanging bullet on a heading, so that you can change it to something else with `::marker`. The following example shows a heading using `display: list-item` for styling purposes, with a list using correct list markup.

  CodePen Embed - Learn CSS: Lists - display-list  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

While you can turn anything into a list-item view with `display`, you shouldn't use this instead of using correct list markup, if the content you are styling really is a list. Changing the visual appearance of an item to a list item does not change how accessibility services read and recognize the item, so it won't be read as a list item to screen readers or switch devices. You should always use semantic markup and create lists with `<li>` whenever possible.

### Check your understanding

Test your knowledge of lists

The element preceding a list-item is called a

The three types of HTML lists are

Which two styles in this list will apply styles to a `::marker`?

## Resources

*   [MDN Guide on Styling Lists](https://developer.mozilla.org/docs/Learn/CSS/Styling_text/Styling_lists)
*   [Custom bullets with CSS ::marker](https://web.dev/articles/css-marker-pseudo-element)
*   [Smashing Magazine: CSS Lists, Markers and Counters](https://www.smashingmagazine.com/2019/07/css-lists-markers-counters/)
*   [MDN Using CSS Counters](https://developer.mozilla.org/docs/Web/CSS/CSS_Lists_and_Counters/Using_CSS_counters)
*   [CSS Lists and Counters Module Level 3](https://www.w3.org/TR/css-lists-3/)
*   [CSS-Tricks: Counting With CSS Counters and CSS Grid](https://css-tricks.com/counting-css-counters-css-grid/)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
