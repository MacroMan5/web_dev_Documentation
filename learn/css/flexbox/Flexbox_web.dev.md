# Flexbox  |  web.dev

**Source URL:** [https://web.dev/learn/css/flexbox?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Fflexbox](https://web.dev/learn/css/flexbox?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Fflexbox)  
**Last Updated:** 2025-05-23T01:08:07.673Z  
**Extracted:** 2025-05-31 16:58:10

---

# Flexbox  |  web.dev

##### [The CSS Podcast - 010: Flexbox](https://thecsspodcast.libsyn.com/010-flexbox)

A design pattern that can be tricky in responsive design is a sidebar that sits inline with some content. Where there is viewport space, this pattern works great, but where space is condensed, that rigid layout can become problematic.

  CodePen Embed - Learn CSS - Flexbox - Intro  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

The Flexible Box Layout Model (flexbox) is a layout model designed for one-dimensional content. It excels at taking a bunch of items which have different sizes, and returning the best layout for those items.

This is the ideal layout model for this sidebar pattern. Flexbox not only helps lay the sidebar and content out inline, but where there's not enough space remaining, the sidebar will break onto a new line. Instead of setting rigid dimensions for the browser to follow, with flexbox, you can instead provide flexible boundaries to hint how the content could display.

  CodePen Embed - Learn CSS - Flexbox - Intro 2  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## What can you do with a flex layout?

Flex layouts have the following features, which you will be able to explore in this guide.

*   They can display as a row, or a column.
*   They respect the writing mode of the document.
*   They are single line by default, but can be asked to wrap onto multiple lines.
*   Items in the layout can be visually reordered, away from their order in the DOM.
*   Space can be distributed inside the items, so they become bigger and smaller according to the space available in their parent.
*   Space can be distributed around the items and flex lines in a wrapped layout, using the Box Alignment properties.
*   The items themselves can be aligned on the cross axis.

## The main axis and the cross axis

The key to understanding flexbox is to understand the concept of a main axis and a cross axis. The main axis is the one set by your `flex-direction` property. If that is `row` your main axis is along the row, if it is `column` your main axis is along the column.

![Three boxes next to each other with an arrow, pointing left to right. The arrow is labelled Main axis](https://web.dev/static/learn/css/flexbox/image/three-boxes-next-each-w-7b5d0fbdaf522.svg)

Flex items move as a group on the main axis. Remember: we've got a bunch of things and we are trying to get the best layout for them as a group.

The cross axis runs in the other direction to the main axis, so if `flex-direction` is `row` the cross axis runs along the column.

![Three boxes of different heights, next to each other with an arrow, pointing left to right. The arrow is labelled Main axis. There's another arrow pointing top to bottom. This one is labelled Cross axis](https://web.dev/static/learn/css/flexbox/image/three-boxes-different-he-20fd54d77efbb.svg)

You can do two things on the cross axis. You can move the items individually or as a group, so they align against each other and the flex container. Also, if you have wrapped flex lines, you can treat those lines as a group to control how space is assigned to those lines. You will see how this all works in practice throughout this guide, for now just keep in mind that the main axis follows your `flex-direction`.

## Creating a flex container

Let's see how flexbox behaves by taking a group of different sized items and using flexbox to lay them out.

```
<div class="container" id="container">
  <div>One</div>
  <div>Item two</div>
  <div>The item we will refer to as three</div>
</div>
```

To use flexbox you need to declare that you want to use a flex formatting context and not regular block and inline layout. Do this by changing the value of the `display` property to `flex`.

```
.container {
  display: flex;
}
```

As you learned in the [layout guide](https://web.dev/learn/css/layout) this will give you a block-level box, with flex item children. The flex items immediately start exhibiting some flexbox behavior, using their **initial values**.

The initial values mean that:

*   Items display as a row.
*   They do not wrap.
*   They do not grow to fill the container.
*   They line up at the start of the container.

## Controlling the direction of items

Even though you haven't added a `flex-direction` property yet, the items display as a row because the initial value of `flex-direction` is `row`. If you want a row then you don't need to add the property. To change the direction, add the property and one of the four values:

*   `row`: the items lay out as a row.
*   `row-reverse:` the items lay out as a row from the end of the flex container.
*   `column`: the items lay out as a column.
*   `column-reverse` : the items lay out as a column from the end of the flex container.

You can try out all of the values using our group of items in the demo below.

  CodePen Embed - Learn CSS - Flexbox - Flex direction property  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Reversing the flow of items and accessibility

You should be cautious when using any properties that reorder the visual display away from how things are ordered in the HTML document, as it can negatively impact accessibility. The `row-reverse` and `column-reverse` values are a good example of this. The reordering only happens for the visual order, not the logical order. This is important to understand as the logical order is the order that a screen reader will read out the content, and anyone navigating using the keyboard will follow.

You can see in the following video how in a reversed row layout, tabbing between links becomes disconnected as the keyboard navigation follows the DOM not the visual display.

Anything which can change the order of items in flexbox or grid can cause this problem. Therefore any reordering should include thorough testing to check that it will not make your site hard to use for some people.

For more information see:

*   [Content reordering](https://web.dev/articles/content-reordering)
*   [Flexbox and the keyboard navigation disconnect](https://tink.uk/flexbox-the-keyboard-navigation-disconnect/)

### Writing modes and direction

Flex items lay out as a row by default. A row runs in the direction that sentences flow in your writing mode and script direction. This means that if you are working in Arabic, which has a right-to-left (rtl) script direction, the items will line up on the right. Tab order would also begin on the right as this is the way sentences are read in Arabic.

  CodePen Embed - Learn CSS - Flex items with RTL direction  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

If you are working with a vertical writing mode, like some Japanese typefaces, then a row will run vertically, from top to bottom. Try changing the `flex-direction` in this demo which is using a vertical writing mode.

  CodePen Embed - Learn CSS - Flexbox - Vertical writing mode example  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Therefore the way flex items behave by default is linked to the writing mode of the document. Most tutorials are written using English, or another horizontal, left to right writing mode. This would make it easy to assume that flex items line up **on the left**, and run **horizontally**.

With the main and cross axis plus the writing mode to consider, the fact that we talk about **start** and **end** rather than top, bottom, left, and right in flexbox might be easier to understand. Each axis has a start and an end. The start of the main axis is referred to as **main-start**. So our flex items initially line up from main-start. The end of that axis is **main-end**. The start of the cross axis is **cross-start** and the end **cross-end**.

![A labelled diagram of the above terms](https://web.dev/static/learn/css/flexbox/image/a-labelled-diagram-the-a-a9bf061b5d5b2.svg)

## Wrapping flex items

The initial value of the `flex-wrap` property is `nowrap`. This means that if there is not enough space in the container the items will overflow.

![A flex container with nine items inside it, the items have shrunk down so one word is on a line
but there is not enough room to show them side by side so the flex items have extended outside the
box of the container.](https://web.dev/static/learn/css/flexbox/image/a-flex-container-nine-it-e0d8b646b8c9c.jpg)

Once they hit min-content size flex items will start to overflow their container

Items displaying using the initial values will shrink as small as they can, down to the `min-content` size before overflow happens.

To cause the items to wrap add `flex-wrap: wrap` to the flex container.

```
.container {
  display: flex;
  flex-wrap: wrap;
}
```

  CodePen Embed - Learn CSS - Flexbox - Wrapped flex lines  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

When a flex container wraps it creates multiple **flex lines**. In terms of space distribution, each line acts like a new flex container. Therefore if you are wrapping rows, it is not possible to get something in row 2 to line up with something above it in row 1. This is what is meant by flexbox being one-dimensional. You can control alignment in one axis, a row or a column, not both together as we can do in grid.

### The flex-flow shorthand

You can set the `flex-direction` and `flex-wrap` properties using the shorthand `flex-flow`. For example, to set `flex-direction` to `column` and allow items to wrap:

```
.container {
  display: flex;
  flex-flow: column wrap;
}
```

## Controlling space inside flex items

Assuming our container has more space than is needed to display the items, the items line up at the start and do not grow to fill the space. They stop growing at their max-content size. This is because the initial value of the `flex-` properties is:

*   `flex-grow: 0`: items do not grow.
*   `flex-shrink: 1`: items can shrink smaller than their [`flex-basis`](https://developer.mozilla.org/docs/Web/CSS/flex-basis).
*   `flex-basis: auto`: items have a base size of `auto`.

This can be represented by a keyword value of `flex: initial`. The `flex` shorthand property, or the longhands of `flex-grow`, `flex-shrink` and `flex-basis` are applied to the children of the flex container.

  CodePen Embed - Learn CSS - Flexbox - Flex property  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

To cause the items to grow, while allowing large items to have more space than small ones use `flex:auto`. You can try this using the demo above. This sets the properties to:

*   `flex-grow: 1`: items can grow larger than their `flex-basis`.
*   `flex-shrink: 1`: items can shrink smaller than their `flex-basis`.
*   `flex-basis: auto`: items have a base size of `auto`.

Using `flex: auto` will mean that items end up different sizes, as the space that is shared between the items is shared out _after_ each item is laid out as max-content size. So a large item will gain more space. To force all of the items to be a consistent size and ignore the size of the content change `flex:auto` to `flex: 1` in the demo.

This unpacks to:

*   `flex-grow: 1`: items can grow larger than their `flex-basis`.
*   `flex-shrink: 1`: items can shrink smaller than their `flex-basis`.
*   `flex-basis: 0`: items have a base size of `0`.

Using `flex: 1` says that all items have zero size, therefore all of the space in the flex container is available to be distributed. As all items have a `flex-grow` factor of `1` they all grow equally and the space is shared equally.

### Allowing items to grow at different rates

You don't have to give all items a `flex-grow` factor of `1`. You could give your flex items different `flex-grow` factors. In the demo below the first item has `flex: 1`, the second `flex: 2` and third `flex: 3`. As these items grow from `0` the available space in the flex container is shared into six. One part is given to the first item, two parts to the second, three parts to the third.

  CodePen Embed - Learn CSS - Flexbox - Flex grow  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

You can do the same thing from a `flex-basis` of `auto`, though you will need to specify the three values. The first value being `flex-grow`, the second `flex-shrink`, and the third `flex-basis`.

```
.item1 {
  flex: 1 1 auto;
}

.item2 {
  flex: 2 1 auto;
}
```

This is a less common use case as the reason to use a `flex-basis` of `auto` is to allow the browser to figure out space distribution. If you wanted to cause an item to grow a little more than the algorithm decides however it might be useful.

## Reordering flex items

Items in your flex container can be reordered using the `order` property. This property allows the ordering of items in **ordinal groups**. Items are laid out in the direction dictated by `flex-direction`, lowest values first. If more than one item has the same value it will be displayed with the other items with that value.

The example below demonstrates this ordering.

  CodePen Embed - Learn CSS - Flexbox - Order property  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Check your understanding

Test your knowledge of flexbox

The default `flex-direction` is

By default, a flex container wraps children.

A flex child item appears squished, which flex property helps mitigate this?

## Flexbox alignment overview

Flexbox brought with it a set of properties for aligning items and distributing space between items. These properties were so useful they have since been moved into their own specification, you'll encounter them in Grid Layout too. Here you can find out how they work when you are using flexbox.

The set of properties can be placed into two groups. Properties for space distribution, and properties for alignment. The properties which distribute space are:

*   `justify-content`: space distribution on the main axis.
*   `align-content`: space distribution on the cross axis.
*   `place-content`: a shorthand for setting both of the above properties.

The properties used for alignment in flexbox:

*   `align-self`: aligns a single item on the cross axis.
*   `align-items`: aligns all of the items as a group on the cross axis.

If you are working on the main axis then the properties begin with `justify-`. On the cross axis they begin with `align-`.

## Distributing space on the main axis

With the HTML used earlier, the flex items laid out as a row, there is space on the main axis. The items are not big enough to completely fill the flex container. The items line up at the start of the flex container because the initial value of `justify-content` is `flex-start`. The items line up at the start and any extra space is at the end.

Add the `justify-content` property to the flex container, give it a value of `flex-end`, and the items line up at the end of the container and the spare space is placed at the start.

```
.container {
  display: flex;
  justify-content: flex-end;
}
```

You can also distribute the space between the items with `justify-content: space-between`.

Try some of the values in the demo, and [see MDN](https://developer.mozilla.org/docs/Web/CSS/justify-content) for the full set of possible values.

  CodePen Embed - Learn CSS - Flexbox - Justify content  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### With `flex-direction: column`

If you have changed your `flex-direction` to `column` then `justify-content` will work on the column. To have spare space in your container when working as a column you need to give your container a `height` or `block-size`. Otherwise you won't have spare space to distribute.

Try the different values, this time with a flexbox column layout.

  CodePen Embed - Learn CSS - Flexbox - Justify content  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Distributing space between flex lines

With a wrapped flex container you might have space to distribute on the cross axis. In this case you can use the `align-content` property with the same values as `justify-content`. Unlike `justify-content` which aligns items to `flex-start` by default, the initial value of `align-content` is `stretch`. Add the property `align-content` to the flex container to change that default behavior.

```
.container {
  align-content: center;
}
```

Try this out in the demo. The example has wrapped lines of flex items, and the container has a `block-size` in order that we have some spare space.

  CodePen Embed - Learn CSS - Flexbox - Align content  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### The `place-content` shorthand

To set both `justify-content` and `align-content` you can use `place-content` with one or two values. A single value will be used for both axes, if you specify both the first is used for `align-content` and the second for `justify-content`.

```
.container {
  place-content: space-between;
  /* sets both to space-between */
}

.container {
  place-content: center flex-end;
  /* wrapped lines on the cross axis are centered,
  on the main axis items are aligned to the end of the flex container */
}
```

## Aligning items on the cross-axis

On the cross axis you can also align your items within the flex line using `align-items` and `align-self`. The space available for this alignment will depend on the height of the flex container, or flex line in the case of a wrapped set of items.

The initial value of `align-self` is `stretch`, which is why flex items in a row stretch to the height of the tallest item by default. To change this, add the `align-self` property to any of your flex items.

```
.container {
  display: flex;
}

.item1 {
  align-self: flex-start;
}
```

Use any of the following values to align the item:

*   `flex-start`
*   `flex-end`
*   `center`
*   `stretch`
*   `baseline`

See [the full list of values on MDN](https://developer.mozilla.org/docs/Web/CSS/align-self).

The next demo has a single line of flex items with `flex-direction: row`. The last item defines the height of the flex container. The first item has the `align-self` property with a value of `flex-start`. Try changing the value on that property to see how it moves within its space on the cross axis.

  CodePen Embed - Learn CSS - Flexbox - The align-self property  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

The `align-self` property is applied to individual items. The `align-items` property can be applied to the flex container to set all of the individual `align-self` properties as a group.

```
.container {
  display: flex;
  align-items: flex-start;
}
```

In this next demo try changing the value of `align-items` to align all of the items on the cross axis as a group.

  CodePen Embed - Learn CSS - Flexbox - Align items  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Why is there no justify-self in flexbox?

Flex items act as a group on the main axis. So there is no concept of splitting an individual item out of that group.

In grid layout the `justify-self` and `justify-items` properties work on the inline axis to do alignment of items on that axis within their grid area. Due to the way that flex layouts treat items as a group, these properties are not implemented in a flex context.

It is worth knowing that flexbox does work very nicely with auto margins. If you come across a need to split off one item from a group, or separate the group into two groups you can apply a margin to do this. In the example below the last item has a left margin of `auto`. The auto margin absorbs all space in the direction it is applied. This means that it pushes the item over to the right, thus splitting the groups.

  CodePen Embed - Learn CSS - Flexbox - Flexbox and auto margins  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## How to center an item vertically and horizontally

The alignment properties can be used to center an item inside another box. The `justify-content` property aligns the item on the main axis, which is row. The `align-items` property on the cross axis.

```
.container {
  width: 400px;
  height: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
}
```

### Check your understanding

Test your knowledge of flexbox

.container {
  display: flex;
  direction: ltr;
}

To vertically align with flexbox, use

.container {
  display: flex;
  direction: ltr;
}

To horizontally align with flexbox, use

.container {
  display: flex;
  direction: ltr;
}

By default, flex items are aligned to `stretch`. If you want content size used for child items, which of the following styles would you use?

`justify-content: flex-start`

## Resources

*   [MDN CSS Flexible Box Layout](https://developer.mozilla.org/docs/Web/CSS/CSS_Flexible_Box_Layout) includes a series of detailed guides with examples.
*   [CSS Tricks Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
*   [What Happens When You Create a Flexbox Flex Container](https://www.smashingmagazine.com/2018/08/flexbox-display-flex-container/)
*   [Everything You Need To Know About Alignment In Flexbox](https://www.smashingmagazine.com/2018/08/flexbox-alignment/)
*   [How Big Is That Flexible Box?](https://www.smashingmagazine.com/2018/09/flexbox-sizing-flexible-box/)
*   [Use Cases For Flexbox](https://www.smashingmagazine.com/2018/10/flexbox-use-cases/)
*   [Inspect and debug CSS Flexbox layouts in Chrome DevTools](https://developer.chrome.com/docs/devtools/css/flexbox)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
