# Functions  |  web.dev

**Source URL:** [https://web.dev/learn/css/functions?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Ffunctions](https://web.dev/learn/css/functions?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Ffunctions)  
**Last Updated:** 2025-05-23T01:10:42.938Z  
**Extracted:** 2025-05-31 16:58:10

---

# Functions  |  web.dev

##### [The CSS Podcast - 020: Functions](https://thecsspodcast.libsyn.com/020-functions)

So far in this course, you've been exposed to several CSS functions. In the [grid](https://web.dev/learn/css/grid) module, you were introduced to `minmax()` and `fit-content()`, which help you size elements. In the [color](https://web.dev/learn/css/color) module, you were introduced to `rgb()`, and `hsl()`, which help you define colors.

Like many other programming languages, [CSS has **a lot** of built-in functions](https://developer.mozilla.org/docs/Web/CSS/CSS_Functions) that you can access whenever you need them.

Every CSS function has a specific purpose, in this lesson, you'll get a high-level overview, giving you a much better understanding of where and how to use them.

## What is a function?

A function is a named, self-contained piece of code that completes a specific task. A function is named so you can call it within your code and you can pass data into the function. This is known as passing arguments.

![A diagram of a function as described above](https://web.dev/static/learn/css/functions/image/a-diagram-a-function-de-e40ae94dbccc1.svg)

A lot CSS functions are _pure functions_, which means that if you pass the same arguments into them, they will always give you the same result back, regardless of what is happening in the rest of your code. These functions will often re-compute as values change in your CSS, similar to other elements in the language, such as computed cascaded values like `currentColor`.

In CSS, you can only use the provided functions, rather than write your own, but functions can be nested within each other in some contexts, giving them more flexibility. We'll cover that in more detail, later in this module.

## Functional selectors

```
.post :is(h1, h2, h3) {
    line-height: 1.2;
}
```

You learned about functional selectors in the [pseudo-classes module](https://web.dev/learn/css/pseudo-classes) which detailed functions like [`:is()`](https://developer.mozilla.org/docs/Web/CSS/:is) and [`:not()`](https://developer.mozilla.org/docs/Web/CSS/:not). The arguments passed into these functions are CSS selectors, which are then evaluated. If there is a match with elements, the rest of the **CSS rule** will be applied to them.

## Custom properties and `var()`

```
:root {
    --base-color: #ff00ff;
}

.my-element {
    background: var(--base-color);
}
```

A custom property is a variable which allows you to tokenize values in your CSS code. [Custom properties are also affected by the cascade](https://piccalil.li/tutorial/getting-started-with-css-custom-properties/) which means they can be contextually manipulated or redefined. A custom property must be prefixed with two dashes (`--`) and are case sensitive.

The [`var()`](https://developer.mozilla.org/docs/Web/CSS/var\(\)) function takes one required argument: the custom property that you are trying to return as a value. In the above snippet, the `var()` function has `--base-color` passed as an argument. If `--base-color` is defined, then `var()` will return the value.

```
.my-element {
    background: var(--base-color, hotpink);
}
```

You can also pass a fallback declaration value into the `var()` function. This means that if `--base-color` can't be found, the passed **declaration** will be used instead, which in this sample's case is the `hotpink` color.

  CodePen Embed - Learn CSS - Custom property fallback  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Functions that return a value

The `var()` function is just one of the CSS functions that return a value. Functions like [`attr()`](https://developer.mozilla.org/docs/Web/CSS/attr\(\)) and [`url()`](https://developer.mozilla.org/docs/Web/CSS/url\(\)) follow a similar structure to `var()`— you pass one or more arguments and use them on the **right side** of your CSS declaration.

```
a::after {
  content: attr(href);
}
```

The `attr()` function here is taking the content of the `<a>` element's `href` attribute and setting it as the `content` of the `::after` pseudo-element. If the value of the `<a>` element's `href` attribute was to change, this would automatically be reflected in this `content` attribute.

```
.my-element {
    background-image: url('/path/to/image.jpg');
}
```

The `url()` function takes a **string** URL and is used to load images, fonts and content. If a valid URL isn't passed in or the resource that the URL points to can't be found, nothing will be returned by the `url()` function.

## Color functions

You learned all about color functions in the [color](https://web.dev/learn/css/color) module. If you haven't read that one yet, it is strongly recommended that you do.

Some available color functions in CSS are `rgb()`, `rgba()`, `hsl()`, `hsla()`, `hwb()`, `lab()` and `lch()`. All of these have a similar form where configuration arguments are passed in and a color is returned back.

## Mathematical expressions

Like many other programming languages, CSS provides useful mathematical functions to assist with various types of calculation.

### calc()

The [`calc()`](https://developer.mozilla.org/docs/Web/CSS/calc\(\)) function takes a single mathematical expression as its parameter. This mathematical expression can be a mix of types, such as length, number, angle and frequency. Units can be mixed too.

```
.my-element {
    width: calc(100% - 2rem);
}
```

In this example, the `calc()` function is being used to size an element's width as 100% of its containing parent element, then removing `2rem` off that computed value.

  CodePen Embed - Learn CSS - Calc function  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

```
:root {
  --root-height: 5rem;
}

.my-element {
  width: calc(calc(10% + 2rem) * 2);
  height: calc(var(--root-height) * 3);
}
```

The `calc()` function can be nested inside another `calc()` function. You can also pass custom properties in a `var()` function as part of an expression.

### `min()` and `max()`

The [`min()`](https://developer.mozilla.org/docs/Web/CSS/min\(\)) function returns the smallest computed value of the one or more passed arguments. The [`max()`](https://developer.mozilla.org/docs/Web/CSS/max\(\)) function does the opposite: get the largest value of the one or more passed arguments.

```
.my-element {
  width: min(20vw, 30rem);
  height: max(20vh, 20rem);
}
```

In this example, the width should be the smallest value between `20vw` —which is 20% of the **viewport width**—and `30rem`. The height should be the largest value between `20vh` —which is 20% of the **viewport height**—and `20rem`.

### clamp()

The [`clamp()`](https://developer.mozilla.org/docs/Web/CSS/clamp\(\)) function takes three arguments: the minimum size, the ideal size and the maximum.

```
h1 {
  font-size: clamp(2rem, 1rem + 3vw, 3rem);
}
```

In this example, the `font-size` will be fluid based on the width of the viewport. The `vw` unit is added to a `rem` unit to assist with screen zooming, because regardless of zoom level a `vw` unit will be the same size. Multiplying by a `rem` unit—based on the root font size— provides the `clamp()` function with a relative calculation point.

You can learn more about the `min()`, `max()`, and `clamp`() functions in [this article](https://web.dev/articles/min-max-clamp).

## Shapes

The [`clip-path`](https://developer.mozilla.org/docs/Web/CSS/clip-path), [`offset-path`](https://developer.mozilla.org/docs/Web/CSS/offset-path) and [`shape-outside`](https://developer.mozilla.org/docs/Web/CSS/shape-outside) CSS properties use shapes to visually clip your box or provide a shape for content to flow around.

There are shape functions that can be used with both of these properties. Simple shapes such as [`circle()`](https://developer.mozilla.org/docs/Web/CSS/basic-shape/circle\(\)), [`ellipse()`](https://developer.mozilla.org/docs/Web/CSS/basic-shape/ellipse\(\)) and [`inset()`](https://developer.mozilla.org/docs/Web/CSS/basic-shape/inset\(\)) take configuration arguments to size them. More complex shapes, such as [`polygon()`](https://developer.mozilla.org/docs/Web/CSS/basic-shape/polygon\(\)) take comma separated pairs of X and Y axis values to create custom shapes.

```
.circle {
  clip-path: circle(50%);
}

.polygon {
  clip-path: polygon(0% 0%, 100% 0%, 100% 75%, 75% 75%, 75% 100%, 50% 75%, 0% 75%);
}
```

  CodePen Embed - Learn CSS - Clip path  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Like `polygon()`, there is also a `path()` function which takes an SVG fill rule as an argument. This allows for highly complex shapes that can be drawn in a graphics tool such as Illustrator or Inkscape and then copied into your CSS.

## Transforms

Lastly in this overview of CSS functions are the transform functions, which skew, resize and even change the depth of an element. All of the following functions are used with the `transform` property.

### Rotation

You can rotate an element using the [`rotate()`](https://developer.mozilla.org/docs/Web/CSS/transform-function/rotate\(\)) function, which will rotate an element on its center axis. You can also use the [`rotateX()`](https://developer.mozilla.org/docs/Web/CSS/transform-function/rotateX\(\)), [`rotateY()`](https://developer.mozilla.org/docs/Web/CSS/transform-function/rotateY\(\)) and [`rotateZ()`](https://developer.mozilla.org/docs/Web/CSS/transform-function/rotateZ\(\)) functions to rotate an element on a specific axis instead. You can pass degree, turn and radian units to determine the level of rotation.

```
.my-element {
  transform: rotateX(10deg) rotateY(10deg) rotateZ(10deg);
}
```

  CodePen Embed - Learn CSS - The rotate functions  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

The [`rotate3d()`](https://developer.mozilla.org/docs/Web/CSS/transform-function/rotate3d\(\)) function takes four arguments.

The first 3 arguments are numbers, which define the X, Y and Z coordinates. The fourth argument is the rotation which, like the other rotation functions, accepts degrees, angle and turns.

```
.my-element {
  transform: rotate3d(1, 1, 1, 10deg);
}
```

  CodePen Embed - Learn CSS - rotate3d  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Scale

You can change the scaling of an element with `transform` and the [`scale()`](https://developer.mozilla.org/docs/Web/CSS/transform-function/scale\(\)) function. The function accepts one or two numbers as a value which determine a positive or negative scaling. If you only define one number argument, both the X and Y axis will be scaled the same and defining both is a shorthand for X and Y. Just like `rotate()`, there are [`scaleX()`](https://developer.mozilla.org/docs/Web/CSS/transform-function/scaleX\(\)), [`scaleY()`](https://developer.mozilla.org/docs/Web/CSS/transform-function/scaleY\(\)) and [`scaleZ()`](https://developer.mozilla.org/docs/Web/CSS/transform-function/scaleZ\(\)) functions to scale an element on a specific axis instead.

```
.my-element {
  transform: scaleX(1.2) scaleY(1.2);
}
```

  CodePen Embed - Learn CSS - The scale functions  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Also like the `rotate` function, there is a [`scale3d()`](https://developer.mozilla.org/docs/Web/CSS/transform-function/scale3d\(\)) function. This is similar to `scale()`, but it takes three arguments: the X, Y and Z scale factor.

### Translate

The [`translate()`](https://developer.mozilla.org/docs/Web/CSS/transform-function/translate\(\)) functions move an element while it maintains its position in the document flow. They accept length and percentage values as arguments. The `translate()` function translates an element along the X axis if one argument is defined, and translates an element along the X and Y axis if both arguments are defined.

```
.my-element {
  transform: translatex(40px) translatey(25px);
}
```

  CodePen Embed - Learn CSS - Translate functions  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

You can—just like with other transform functions—use specific functions for a specific axis, using [`translateX`](https://developer.mozilla.org/docs/Web/CSS/transform-function/translateX\(\)), [`translateY`](https://developer.mozilla.org/docs/Web/CSS/transform-function/translateY\(\)) and [`translateZ`](https://developer.mozilla.org/docs/Web/CSS/transform-function/translateZ\(\)). You can also use [`translate3d`](https://developer.mozilla.org/docs/Web/CSS/transform-function/translate3d\(\)) which allows you to define the X, Y and Z translation in one function.

### Skewing

You can skew an element, using the [`skew()`](https://developer.mozilla.org/docs/Web/CSS/transform-function/skew\(\)) functions which accept angles as arguments. The `skew()` function works in a very similar way to `translate()`. If you only define one argument, it will only affect the X axis and if you define both, it will affect the X and Y axis. You can also use [`skewX`](https://developer.mozilla.org/docs/Web/CSS/transform-function/skewX\(\)) and [`skewY`](https://developer.mozilla.org/docs/Web/CSS/transform-function/skewY\(\)) to affect each axis independently.

```
.my-element {
  transform: skew(10deg);
}
```

  CodePen Embed - Learn CSS - Skew function  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Perspective

Lastly, you can use the [`perspective`](https://developer.mozilla.org/docs/Web/CSS/perspective) property —which is part of the transform family of properties—to alter the distance between the user and the Z plane. This gives the feeling of distance and can be used to create a depth of field in your designs.

This example by David Desandro, from their very useful article, shows how it can be used, along with `perspective-origin-x` and `perspective-origin-y` properties to create truly 3D experiences.

  CodePen Embed - Perspective cube  

Live

Live

Live

[![](https://assets.codepen.io/82/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1538443323&width=256)](https://codepen.io/desandro)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

## Animation functions, gradients and filters

CSS also provides functions that help you [animate](https://web.dev/learn/css/animations) elements, apply [gradients](https://web.dev/learn/css/gradients) to them and use graphical [filters](https://web.dev/learn/css/filters) to manipulate how they look. To keep this module as concise as possible, they are covered in the linked modules. They all follow a similar structure to the functions demonstrated in this module.

### Check your understanding

Test your knowledge of functions

CSS functions can be identified by which characters?

CSS has built-in math functions?

A `calc()` function can be placed inside of another `calc()` like `font-size: calc(10px + calc(5px * 3));`

Which of the following are CSS shape functions?

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
