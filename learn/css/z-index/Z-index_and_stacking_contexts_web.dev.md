# Z-index and stacking contexts  |  web.dev

**Source URL:** [https://web.dev/learn/css/z-index?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Fz-index](https://web.dev/learn/css/z-index?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Fz-index)  
**Last Updated:** 2025-05-23T01:10:30.137Z  
**Extracted:** 2025-05-31 16:58:10

---

# Z-index and stacking contexts | web.dev

Z-index and stacking contexts

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

##### [The CSS Podcast - 019: z-index and stacking contexts](https://thecsspodcast.libsyn.com/019-z-index-and-stacking-context)

Say you've got a couple of elements that are absolutely positioned, and are supposed to be positioned on top of each other. You might write a bit of a HTML like this:

```
<div class="stacked-items">
    <div class="item-1">Item 1</div>
    <div class="item-2">Item 2</div>
</div>
```

But which one sits on top of the other, by default? To know which item would do that, you need to understand z-index and stacking contexts.

The [`z-index`](https://developer.mozilla.org/docs/Web/CSS/z-index) property explicitly sets a layer order for HTML based on the 3D space of the browser—the Z axis. This is the axis which shows which layers are closer to and further from you. The vertical axis on the web is the Y axis and the horizontal axis is the X axis.

![Each axis surrounding the element](https://web.dev/static/learn/css/z-index/image/each-axis-surrounding-el-6a38535cc8004.svg)

The `z-index` property accepts a numerical value which can be a positive or negative number. Elements will appear above another element if they have a higher `z-index` value. If no `z-index` is set on your elements then the default behaviour is that document source order dictates the Z axis. This means that elements further down the document sit on top of elements that appear before them.

  CodePen Embed - Learn CSS - Default z-index behaviour  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

In normal flow, if you set a specific value for `z-index` and it isn't working, you need to set the element's `position` value to anything other than `static`. This is a common place where people struggle with `z-index`.

  CodePen Embed - Learn CSS - Relative positioning and z-index  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

This isn't the case if you are in a flexbox or grid context, though, because you can modify the z-index of flex or grid items without adding `position: relative`.

  CodePen Embed - Learn CSS - Grid layout and z-index  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Negative z-index

To set an element _behind_ another element, add a negative value for `z-index`.

```
.my-element {
    background: rgb(232 240 254 / 0.4);
}

.my-element .child {
    position: relative;
    z-index: -1;
}
```

As long as `.my-element` has the initial value for `z-index` of `auto`, the `.child` element will sit behind it.

  CodePen Embed - Learn CSS - Negative z-index  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Add the following CSS to `.my-element`, and the `.child` element will not sit behind it.

```
.my-element {
  position: relative;
  z-index: 0;
  background: rgb(232 240 254 / 0.4);
}
```

  CodePen Embed - Learn CSS - Negative z-index  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Because `.my-element` now has a `position` value that's not `static` and a `z-index` value that's not `auto`, it has created a new **stacking context**. This means that even if you set `.child` to have a `z-index` of `-999`, it would still not sit behind `.my-parent`.

## Stacking context

A stacking context is a group of elements that have a common parent and move up and down the z axis together.

  CodePen Embed - JjErOXV  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

In this example, the first parent element has a `z-index` of `1`, so creates a new stacking context. Its child element has a `z-index` of `999`. Next to this parent, there is another parent element with one child. The parent has a `z-index` of `2` and the child element also has a `z-index` of `2`. Because both parents create a stacking context, the `z-index` of all children is based on that of their parent.

The `z-index` of elements inside of a stacking context are always relative to the parent's current order in its own stacking context.

## Creating a stacking context

You don't need to apply `z-index` and `position` to create a new [stacking context](https://developer.mozilla.org/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context). You can create a new stacking context by adding a value for properties which create a new composite layer such as `opacity`, `will-change` and `transform`. You can [see a full list of properties here](https://developer.mozilla.org/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context).

To explain what a composite layer is, imagine a web page is a canvas. A browser takes your HTML and CSS and uses these to work out how big to make the canvas. It then paints the page on this canvas. If an element was to change—say, it changes position—the browser then has to go back and re-work out what to paint.

To help with performance, the browser creates new composite layers which are layered on top of the canvas. These are a bit like post-it notes: moving one around and changing it doesn't have a huge impact on the overall canvas. A new composite layer is created for elements with `opacity`, `transform` and `will-change` because these are very likely to change, so the browser makes sure that change is performant as possible by using the GPU to apply style adjustments.

## Resources

*   [Forcing layers](https://surma.dev/things/forcing-layers/)
*   [Animations Guide: Force layer creation](https://web.dev/articles/animations-guide#force)
*   [Understanding z-index](https://ishadeed.com/article/understanding-z-index/)

### Check your understanding

Test your knowledge of z-index

<section>
  <article>1</article>
  <article>2</article>
  <article>3</article>
  <article>4</article>
</section>

Which article is on top by default?

If z-index isn't working, what property should you inspect on your element?

Do flexbox and grid need `position: relative`?

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
