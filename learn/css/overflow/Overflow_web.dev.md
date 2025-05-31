# Overflow  |  web.dev

**Source URL:** [https://web.dev/learn/css/overflow?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Foverflow](https://web.dev/learn/css/overflow?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Foverflow)  
**Last Updated:** 2025-05-23T01:07:26.364Z  
**Extracted:** 2025-05-31 16:58:10

---

# Overflow  |  web.dev

##### [The CSS Podcast - 034: Overflow](https://thecsspodcast.libsyn.com/034-overflow)

When content extends beyond its parent, there are many options for how you can handle it. You can scroll to add additional space, clip the overflowing edges, indicate the cut-off with an ellipsis, and so much more. Overflow is especially important to consider when developing for phone applications and multiple screen sizes.

  CodePen Embed - LearnCSS - Overflow - intro demo  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

There are two different clipping options in CSS; `text-overflow` will help with individual lines of text, and the `overflow` properties will help control overflow in the box model.

## Single line overflow with `text-overflow`

Use the [`text-overflow`](https://developer.mozilla.org/docs/Web/CSS/text-overflow) property on any element that contains text node(s), for example a paragraph, `<p>`. It specifies how the text appears when it doesn’t fit in the available space of the element. All viewable HTML text on a page is in [text nodes](https://developer.mozilla.org/docs/Web/API/Text). To use `text-overflow` you need a single unwrapped line of text, so you must also set `overflow` to `hidden` and have a `white-space` value that prevents wrapping.

```
p {
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
}
```

  CodePen Embed - LearnCSS - Overflow - text-overflow  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Using overflow properties

Overflow properties are set on an element to control what happens when its children need more space than it has available. This can be intentional, like in an interactive map like Google Maps, where a user pans around a large image clipped to a specific size. It can also be unintentional like in a chat application where the user types a lengthy message that doesn’t fit in the text bubble.

  CodePen Embed - LearnCSS - Overflow - intro to window concept  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

You can think of the overflow in two parts. The parent element has a firmly constrained space that will not change. You can think of this as a window. The child elements are content that want more space from the parent. You can think of this as what you are looking through the window at. Managing overflow will help guide how the window frames this content.

  CodePen Embed - LearnCSS - Overflow - element overflow overview  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Scrolling on the vertical and horizontal axis

The `overflow-y` property controls physical overflow along the vertical axis of the device viewport, therefore scrolling up and down.

The `overflow-x` property controls overflow along the horizontal axis of the device viewport, therefore scrolling left and right.

  CodePen Embed - LearnCSS - Overflow - element overflow-x and overflow-y  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Logical properties for scroll direction

The [`overflow-inline`](https://developer.mozilla.org/docs/Web/CSS/overflow-inline) and [`overflow-block`](https://developer.mozilla.org/docs/Web/CSS/overflow-block) properties set the overflow based on the document direction and writing mode.

### The `overflow` shorthand

The [`overflow`](https://developer.mozilla.org/docs/Web/CSS/overflow) shorthand sets both `overflow-x` and `overflow-y` styles in one line:

```
overflow: hidden scroll;
```

If two keywords are specified, the first applies to `overflow-x` and the second to `overflow-y`. Otherwise, both `overflow-x` and `overflow-y` use the same value.

#### Values

Let's take a closer look at the [values and keywords](https://developer.mozilla.org/docs/Web/CSS/overflow#values) available for the `overflow` properties.

`overflow: visible` (default)

Without setting the property, `overflow: visible` is the default value for the web. This ensures that content is never unintentionally hidden and follows the core tenets of "never hide content" or "safe layouts of precise layouts".

`overflow: hidden`

With `overflow: hidden` content is clipped in the specified direction, and no scrollbars are provided to show it.

`overflow: scroll`

`overflow: scroll` enables scrollbars to allow users to scroll through content. Even if content isn't currently overflowing, scrollbars will be present. This is a great way to reduce future layout shift if a container may be scrollable in the future based, for example, on resize, and visually prepare the user for scrollable areas.

`overflow: clip`

Like `overflow: hidden`, the content with `overflow: clip` is clipped to the element's padding box. The difference between `clip` and `hidden` is that the `clip` keyword also forbids all scrolling, including programmatic scrolling.

`overflow: auto`

Finally, the value most commonly used, `overflow: auto`. This respects the user's preferences and shows scrollbars if needed, but hides them by default, and gives responsibility for scrolling to the user and browser.

  CodePen Embed - LearnCSS - Overflow - overflow  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Many of these `overflow` behaviors introduce a scrollbar, but there’s a few specific scroll behaviors and properties that can help you control scrolling on your overflow container.

### Scrolling and accessibility

It's important to make sure that the scrollable area can accept focus so that a keyboard user can tab to the box, then use the arrow keys to scroll.

To allow a scrolling box to accept focus add `tabindex="0"`, a name with the [`aria-labelledby`](https://developer.mozilla.org/docs/Web/Accessibility/ARIA/Attributes/aria-labelledby) attribute, and an appropriate `role` attribute. For example:

```
<div tabindex="0" role="region" aria-labelledby="id-of-descriptive-text">
    content
</div>
```

CSS can then be used to indicate that the box has focus, using the `outline` property to give a visual clue that it will now be scrollable.

In [Using CSS to Enforce Accessibility](https://adrianroselli.com/2021/06/using-css-to-enforce-accessibility.html) Adrian Roselli demonstrates how CSS can help prevent accessibility regressions. For example, to only turn on scrolling and add the focus indicator if the correct attributes are used. The following rules will only make the box scrollable if it has a `tabindex`, `aria-labelledby`, and `role` attribute.

```
[role][aria-labelledby][tabindex] {
  overflow: auto;
}

[role][aria-labelledby][tabindex]:focus {
  outline: .1em solid blue;
}
```

### Scrollbar positioning within the box model

Scroll bars take up space within the padding box and can compete for space if `inline` and not `overlaid`. The [box model module](https://web.dev/learn/css/box-model#the_areas_of_the_box_model) expands more on this potential source of layout shift.

  CodePen Embed - Box Model  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

### root-scroller vs implicit-scroller

You may notice that some scrollers have a pull-to-refresh behavior and other special behaviors, especially when developing for mobile and hybrid applications. This scroll behavior happens on the root scroller. There is only ever one root scroller on a page. By default, the [documentElement](https://developer.mozilla.org/docs/Web/API/Document/documentElement) is the page's root scroller, however, by changing which element is the root scroller, the special behaviors can be applied to scrollers other than the documentElement, we call this new scroller the implicit root scroller.

To create a root scroller, you can use something called _scroller promotion_ by positioning a container as fixed, ensuring it covers the entire viewport and is z-index on top with a scroller. Experience a root scroller vs a nested implicit scroller [here](https://cdpn.io/web-dot-dev/debug/dyzPzwz).

The video shows a root scroller with bounce behavior and new styling features,  
compared to scrolling an implicit scroller with no enhanced scroll behavior.

### scroll-behavior

`scroll-behavior` allows you to opt into browser-controlled scrolling to elements. This allows you to specify how in-page navigation like `.scrollTo()` or links are handled.

This is especially useful when used with [prefers-reduced-motion](https://developer.mozilla.org/docs/Web/CSS/@media/prefers-reduced-motion) to specify scroll behavior based on user preference.

```
@media (prefers-reduced-motion: no-preference) {
  .scroll-view {
    scroll-behavior: auto;
  }
}
```

  CodePen Embed - LearnCSS - Overflow - scroll behavior  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### overscroll-behavior

If you’ve ever reached the end of a modal overlay, then continued scrolling and had the page behind the overlay move, this is the scroll chaining, or bubbling up to the parent scroll container. The [`overscroll-behavior`](https://developer.mozilla.org/docs/Web/CSS/overscroll-behavior) property allows you to prevent overflow scrolling leaking into a parent container (called scroll chaining).

  CodePen Embed - LearnCSS - Overflow - overscroll-behavior  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Check your understanding

Test your knowledge of overflow

Text overflow and element overflow are the same?

The `overflow` property accepts 2 keywords, the first keyword is for which axis?

Which space in the box model do scrollbars consume when showing and inline?

To trap extra momentum from scrolling in a nested implicit scroller, which property would you use?

## Resources

[Overflow And Data Loss In CSS from Smashing Magazine](https://www.smashingmagazine.com/2019/09/overflow-data-loss-css/)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
