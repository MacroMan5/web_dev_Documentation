# Logical Properties  |  web.dev

**Source URL:** [https://web.dev/learn/css/logical-properties?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Flogical-properties](https://web.dev/learn/css/logical-properties?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Flogical-properties)  
**Last Updated:** 2025-05-23T01:09:27.739Z  
**Extracted:** 2025-05-31 16:58:10

---

# Logical Properties  |  web.dev

##### [The CSS Podcast - 012: Logical Properties](https://thecsspodcast.libsyn.com/012-logical-properties)

A really common user interface pattern is a text label with a supporting inline icon.

  CodePen Embed - Learn CSS - Logical Properties - Intro 1  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

The icon sits to the left of the text with a small gap between the two, provided by `margin-right` on the icon. There's a problem though, because this will only work when the text direction is left to right. If the text direction changed to right-to-left—which is how languages like Arabic read—the icon will sit up against the text.

  CodePen Embed - Learn CSS - Logical Properties - Intro 2  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

How do you account for this in CSS? Logical properties allow you to resolve these situations. Among many other benefits, they provide free, automatic support for internationalization. They help you build a more resilient, inclusive front-end.

## Terminology

The physical properties of top, right, bottom, and left refer to the physical dimensions of the viewport. You can think of these like a compass rose on a map. Logical properties, on the other hand, refer to the edges of a box as they relate to the _flow of content_. Therefore, they can change if the text direction or writing mode changes. This is a big shift from directional styles, and it gives us a lot more flexibility when styling our interfaces.

## Block flow

Block flow is the direction in which content blocks are placed. For example, if there are two paragraphs, the block flow is where the second paragraph will go. In an English document, the block flow is top-to-bottom. Think of this in the context of paragraphs of text following each other, top-to-bottom.

![Three blocks, div elements, with a down arrow, labelled 'block flow'](https://web.dev/static/learn/css/logical-properties/image/three-blocks-div-element-c412fe2ea9144.svg)

## Inline flow

The inline flow is how text flows in a sentence. In an English document the inline flow is left to right. If you were to change the document language of your webpage to Arabic (`<html lang="ar">`), then the inline flow would be right-to-left.

![Three words, 'she sells seashells', with a left-to-right arrow, labelled 'inline flow'](https://web.dev/static/learn/css/logical-properties/image/three-words-sells-seas-0e2d07a07729b.svg)

Text flows in the direction determined by the document's writing mode. You can change the direction that text is laid out with the `writing-mode` property. This can be applied to the entire document, or to individual elements.

  CodePen Embed - Learn CSS - Writing modes  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Flow relative

Historically in CSS, we have only been able to apply properties like margin relative to the direction of their sides. For example, `margin-top` is applied to the physical top of the element. With logical properties, `margin-top` becomes `margin-block-start`. This means that regardless of language and text direction, the **block flow** has appropriate margin rules.

  CodePen Embed - Learn CSS - Flow relative margin  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

![A diagram showing all the different sizes of a box and where each sizing section starts and ends](https://web.dev/static/learn/css/logical-properties/image/a-diagram-showing-the-di-12ce9bdac4132.png)

## Sizing

To prevent an element exceeding a certain width or height, write a rule like this:

```
.my-element {
  max-width: 150px;
  max-height: 100px;
}
```

The flow-relative equivalents are `max-inline-size` and `max-block-size`. You can also use `min-block-size` and `min-inline-size` instead of `min-height` and `min-width`.

With logical properties, that max width and height rule would look like this:

```
.my-element {
  max-inline-size: 150px;
  max-block-size: 100px;
}
```

## Start and end

Instead of using directions such as top, right, bottom and left, use start and end. This gives you block-start, inline-end, block-end, and inline-start. These allow you to apply CSS properties that respond to writing mode changes.

For example, to align text to the right, you could use this CSS:

```
p {
  text-align: right;
}
```

If your aim is not to align to the physical right, but rather to the start of the reading direction, this isn't helpful. With logical values, there are more helpful `start` and `end` values which map to the text direction. The text alignment rule now looks like this:

```
p {
  text-align: end;
}
```

  CodePen Embed - Learn CSS - start and end, text align  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Spacing and positioning

Logical properties for `margin`, `padding` and `inset` make positioning elements, and determining how these elements interact with each other across writing modes easier and more efficient. The margin and padding related properties are still direct mappings to directions, but the key difference is that when a writing mode changes, they change with it.

```
.my-element {
  padding-top: 2em;
  padding-bottom: 2em;
  margin-left: 2em;
  position: relative;
  top: 0.2em;
}
```

This adds some vertical inside space with `padding` and pushes it out from the left with `margin`. The `top` property also shifts it downwards. With logical property equivalents, it would instead look like this:

```
.my-element {
  padding-block-start: 2em;
  padding-block-end: 2em;
  margin-inline-start: 2em;
  position: relative;
  inset-block-start: 0.2em;
}
```

This adds some inline inside space with `padding` and pushes it out from the inline-start with `margin`. The `inset-block` property moves it inwards from the block-start.

The `inset-block` property isn't the only shorthand option with logical properties. This rule can be further condensed, using shorthand versions of the margin and padding properties.

```
.my-element {
  padding-block: 2em;
  margin-inline: 2em 0;
  position: relative;
  inset-block: 0.2em 0;
}
```

## Borders

Adding `border` and `border-radius` can also be done with logical properties. To add a border on the bottom and right, with a right-hand radius, you might write a rule like this:

```
.my-element {
  border-bottom: 1px solid red;
  border-right: 1px solid red;
  border-bottom-right-radius: 1em;
}
```

Or, you could use logical properties like this:

```
.my-element {
  border-block-end: 1px solid red;
  border-inline-end: 1px solid red;
  border-end-end-radius: 1em;
}
```

The `end-end` in `border-end-end-radius` is the block end _and_ inline end.

  CodePen Embed - Learn CSS - Logical properties and borders  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Units

Logical properties bring two new units: `vi` and `vb`. A `vi` unit is 1% of the viewport size in the inline direction. The non-logical property equivalent is `vw`. The `vb` unit is 1% of the viewport in the block direction. The non-logical property equivalent is `vh`.

These units will always map to the reading direction. For example, if you want an element to take up 80% of the available inline space of a viewport, using the `vi` unit will automatically switch that size to be top to bottom if the writing mode is vertical.

## Using logical properties pragmatically

Logical properties and writing modes are not just for internationalization. You can use them to produce a more versatile user interface.

If you have a chart that has labels on the X axis and Y axis, you might want the text on the Y label to read vertically.

  CodePen Embed - Learn CSS - Logical Properties - Chart  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Because the Y axis label in the demo has a `writing-mode` of `vertical-rl`, you can use the same `margin` values on both labels. The `margin-block-start` value applies to both labels because the block start is on the right for the Y axis and on the top for the X axis. The block-start sides have a red border so you can see them.

## Solving the icon issue

Now that we've covered logical properties, this knowledge can be applied to the design problem we started with.

  CodePen Embed - Learn CSS - Logical Properties - Intro 1  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

```
p {
  display: inline-flex;
  align-items: center;
}

p svg {
  width: 1.2em;
  height: 1.2em;
  margin-right: 0.5em;
  flex: none;
}
```

The margin has been applied to the right of the icon element. In order for the spacing between the icon and the text to support all reading direction, the `margin-inline-end` property needs to be used instead.

```
p {
  display: inline-flex;
  align-items: center;
}

p svg {
  width: 1.2em;
  height: 1.2em;
  margin-inline-end: 0.5em;
  flex: none;
}
```

  CodePen Embed - Learn CSS - Logical Properties - Intro 1  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Now, regardless of reading direction, the icon will position itself and space itself appropriately.

### Check your understanding

Test your knowledge of logical properties

As you write with your hand, your wrist is moving along which logical axis?

Check all that can benefit from logical properties

Which logical side of a word is underlined?

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
