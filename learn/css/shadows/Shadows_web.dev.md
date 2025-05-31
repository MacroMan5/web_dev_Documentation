# Shadows  |  web.dev

**Source URL:** [https://web.dev/learn/css/shadows?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Fshadows](https://web.dev/learn/css/shadows?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Fshadows)  
**Last Updated:** 2025-05-23T01:10:08.886Z  
**Extracted:** 2025-05-31 16:58:10

---

# Shadows  |  web.dev

Shadows

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

##### [The CSS Podcast - 017: Shadows](https://thecsspodcast.libsyn.com/017-shadows)

Say you've been sent a design to build and in that design there's a picture of a t-shirt, cut out, with a drop shadow. The designer tells you that the product image is dynamic and can be updated via the content management system, so the drop shadow needs to be dynamic too. Instead of a t-shirt, the image could be a visor or shorts, or any other item. How do you do that with CSS?

  CodePen Embed - Learn CSS - Shadows intro 1  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

CSS has the [`box-shadow`](https://developer.mozilla.org/docs/Web/CSS/box-shadow) and [`text-shadow`](https://developer.mozilla.org/docs/Web/CSS/text-shadow) properties, but the picture isn't text, so you can't use `text-shadow`. If you use `box-shadow`, the shadow is on the surrounding box, _not_ around the t-shirt.

  CodePen Embed - Learn CSS - Shadows intro 1  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Luckily, there is another option: the [`drop-shadow()`](https://developer.mozilla.org/docs/Web/CSS/filter-function/drop-shadow\(\)) filter. This enables you to do exactly what the designer asked for. There are plenty of options when it comes to shadows in CSS, each designed for a different use case.

## Box shadow

The `box-shadow` property is for adding shadows to the box of an HTML element. It works on block elements and inline elements.

```
.my-element {
    box-shadow: 5px 5px 20px 5px #000;
}
```

The order of values for `box-shadow` are as follows:

1.  **Horizontal offset**: a positive number pushes it out from the left and a negative number will push it out from the right.
2.  **Vertical offset**: a positive number pushes it down from the top, and a negative number will push it up from the bottom.
3.  **Blur radius**: a larger number produces a more blurred shadow, whereas a small number produces a sharper shadow.
4.  **Spread radius** (optional): a larger number increases the size of the shadow and a smaller number decreases it, making it the same size as the **blur radius** if it's set to 0.
5.  **Color**: [Any valid color value](https://web.dev/learn/css/color). If this isn't defined, the computed text color will be used.

To make a box shadow an inner shadow, rather than the default outer shadow, add an `inset` keyword **before** the other properties.

```
/* Outer shadow */
.my-element {
    box-shadow: 5px 5px 20px 5px #000;
}

/* Inner shadow */
.my-element {
    box-shadow: inset 5px 5px 20px 5px #000;
}
```

  CodePen Embed - Learn CSS - Box shadow playground  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Multiple shadows

You can add as many shadows as you like with `box-shadow`. Add a comma separated collection of value sets to achieve this:

```
.my-element {
  box-shadow: 5px 5px 20px 5px darkslateblue, -5px -5px 20px 5px dodgerblue,
    inset 0px 0px 10px 2px darkslategray, inset 0px 0px 20px 10px steelblue;
}

```

  CodePen Embed - Learn CSS - Multiple shadows  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Properties affecting box-shadow

Adding a `border-radius` to your box will also affect the shape of the box shadow. This is because CSS is creating a shadow based on the shape of the box as if light is pointing at it.

```
.my-element {
  box-shadow: 0px 0px 20px 5px darkslateblue;
  border-radius: 25px;
}
```

  CodePen Embed - Learn CSS - Radius shadow  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

If your box with `box-shadow` is in a container that has `overflow: hidden`, the shadow **won't** break out of that overflow either.

```
<div class="my-parent">
  <div class="my-shadow">My shadow is hidden by my parent.</div>
</div>
```
```
.my-parent,
.my-shadow {
  width: 250px;
  height: 250px;
}

.my-shadow {
  box-shadow: 0px 0px 20px 5px darkslateblue;
}

.my-parent {
  overflow: hidden;
}
```

  CodePen Embed - Learn CSS - Hidden shadow  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Text shadow

The `text-shadow` property is very similar to the `box-shadow` property. It only works on text nodes.

```
.my-element {
  text-shadow: 3px 3px 3px hotpink;
}
```

The values for `text-shadow` are the same as `box-shadow` and in the same order. The only difference is that `text-shadow` has no `spread` value and no `inset` keyword.

  CodePen Embed - Learn CSS - Text shadow playground  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

When you add a `box-shadow` it is clipped to the shape of your box, but `text-shadow` has no clipping. This means that if your text is fully or semi transparent, the shadow is visible through it.

```
.my-element {
  text-shadow: 3px 3px 3px gold;
  color: rgb(0 0 0 / 70%);
}
```

  CodePen Embed - Learn CSS - Leaky text shadow  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Multiple shadows

You can add as many shadows as you like with `text-shadow`, just as with `box-shadow`. Add a comma separated collection of value sets, and you can create some really cool text effects, such as 3D text.

```
.my-element {
  text-shadow: 1px 1px 0px white,
    2px 2px 0px firebrick;
  color: darkslategray;
}
```

  CodePen Embed - Learn CSS - Multiple text-shadows  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Drop shadow

To achieve a drop shadow that follows any potential curves of an image, use the CSS `drop-shadow` filter. This shadow is applied to an alpha mask which makes it very useful for adding a shadow to a cutout image, as in the case in the intro of this module.

```
.my-image {
  filter: drop-shadow(0px 0px 10px rgba(0 0 0 / 30%))
}
```

  CodePen Embed - Learn CSS - Drop shadow  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

The `drop-shadow` filter has the same values as `box-shadow` **but** the `inset` keyword and `spread` value are not allowed. You can add as many shadows as you like, by adding multiple instances of `drop-shadow` values to the `filter` property. Each shadow will use the last shadow as a positioning reference point.

  CodePen Embed - Learn CSS - Multiple drop shadows  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Check your understanding

Test your knowledge of shadows

Which shadow value below is unique to `box-shadow`?

Only 13 box shadows allowed on an element at once.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
