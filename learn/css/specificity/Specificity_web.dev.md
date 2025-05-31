# Specificity  |  web.dev

**Source URL:** [https://web.dev/learn/css/specificity?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Fspecificity](https://web.dev/learn/css/specificity?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Fspecificity)  
**Last Updated:** 2025-05-23T01:05:59.840Z  
**Extracted:** 2025-05-31 16:58:10

---

# Specificity  |  web.dev

##### [The CSS Podcast - 003: Specificity](https://thecsspodcast.libsyn.com/003-specificity)

Suppose that you're working with the following HTML and CSS:

```
<button class="branding">Hello, Specificity!</button>
```
```
.branding {
  color: blue;
}

button {
  color: red;
}
```

There's two rules that target the same element here. Each rule contains a declaration that wants to set the color of the button: one tries to color the button red and the other tries to color it blue. Which declaration gets applied to the element?

Understanding the CSS specificity algorithm is the key to understanding how CSS decides between competing declarations.

Specificity is one of the distinct stages of the cascade, which was covered in the last module, on [the cascade](https://web.dev/learn/css/the-cascade).

  CodePen Embed - Learn CSS - Specificity intro  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Specificity scoring

Each selector rule within an [origin](https://web.dev/learn/css/the-cascade#origin) gets a scoring. You can think of specificity as a total score and each selector type earns points towards that score. Declarations from rules with the highest specificity win.

With specificity in a real project, the balancing act is making sure the CSS rules you expect to apply, actually _do apply,_ while generally keeping scores low to prevent complexity. The specificity should only be as high as we need it to be, rather than aiming for the highest specificity possible. In the future, some genuinely more important CSS might need to be applied. If you go for the highest specificity, you'll make that job hard.

The specificity is not a decimal number but a triad that consists of three components: `A`, `B`, and `C`.

*   `A`: id-like specificity
*   `B`: class-like specificity
*   `C`: element-like specificity

It is often represented using the `(A,B,C)` notation. For example: `(1,0,2)`. The alternative `A-B-C` notation is also commonly used.

![A diagram showingthe three components of specificity (A,B,C). For each component, the diagram shows what it represents and some example selectors that affect it.](https://web.dev/static/learn/css/specificity/image/a-diagram-demonstrating-e1f97df6e065a.svg)

A diagram demonstrating what component of specificity various selectors affect.

## Comparing specificities

Specificities are compared by comparing the three components in order: the specificity with a larger A value is more specific; if the two A values are tied, then the specificity with a larger B value is more specific; if the two B values are also tied, then the specificity with a larger C value is more specific; if all the values are tied, the two specificities are equal.

For example, `(1,0,0)` is considered a higher specificity than `(0,4,3)` because the `A` value in `(1,0,0)` (which is `1`) is greater than the `A` value from `(0,4,3)` (which is `0`).

## Selectors influence specificity

Each part in the specificity triad starts with a value of `0`, so the default specificity is `(0,0,0)`. Each part of a selector increases the specificity that, depending on the type of selector, increment the value of either `A`, `B`, or `C`.

### Universal selector

A [universal selector](https://developer.mozilla.org/docs/Web/CSS/Universal_selectors) (`*`) adds **no specificity**, leaving its value at the initial specificity of `(0,0,0)`.

```
* {
  color: red;
}
```

### Element or pseudo-element selector

An [element](https://developer.mozilla.org/docs/Web/CSS/Type_selectors) (type) or [pseudo-element](https://developer.mozilla.org/docs/Web/CSS/Pseudo-elements) selector adds **element-like specificity** which increments the `C` component by `1`.

The following examples have an overall specificity of `(0,0,1)`.

#### Type selector

```
div {
  color: red;
}
```

#### Pseudo-element selector

```
::selection {
  color: red;
}
```

### Class, pseudo-class, or attribute selector

A [class](https://developer.mozilla.org/docs/Web/CSS/Class_selectors), [pseudo-class](https://developer.mozilla.org/docs/Web/CSS/Pseudo-classes) or [attribute](https://developer.mozilla.org/docs/Web/CSS/Attribute_selectors) selector adds **class-like specificity** which increments the `B` component by `1`.

The following examples have a specificity of `(0,1,0)`.

#### Class selector

```
.my-class {
  color: red;
}
```

#### Pseudo-class selector

```
:hover {
  color: red;
}
```

#### Attribute selector

```
[href='#'] {
  color: red;
}
```

### ID selector

An [ID](https://developer.mozilla.org/docs/Web/CSS/ID_selectors) selector adds **id-like specificity** which increments the `A` component by 1, as long as you use an ID selector (`#myID`) and not an attribute selector (`[id="myID"]`).

In the following example, the specificity is `(1,0,0)`

```
#myID {
  color: red;
}
```

### Other selectors

CSS has many selectors. Not all of them add specificity. For example, the [`:not()`](https://developer.mozilla.org/docs/Web/CSS/:not) pseudo-class itself adds nothing to the specificity calculation.

However, the selectors passed in as arguments do get added to the specificity calculation.

```
div:not(.my-class) {
  color: red;
}
```

This sample has a specificity of **(0,1,1)** because it has one type selector (`div`) and one class _inside_ the `:not()`.

### Check your understanding

Test your knowledge of specificity scoring

What is the specificity of `a[href="#"]`?

## Factors that don't affect specificity

There are some common misconceptions about the following factors affecting specificity.

### Inline style attributes

CSS applied directly to the `style` attribute of an element, does not affect specificity as it's a different step in [the cascade](https://web.dev/learn/css/the-cascade) that is evaluated before specificity.

```
<div style="color: red"></div>
```

In order to override this declaration from within a style sheet, you have to resort to get the declaration win in an earlier step of [the cascade](https://web.dev/learn/css/the-cascade).

For example, you could add `!important` to it, so that it becomes part of [the Authored `!important` origin](https://web.dev/learn/css/the-cascade#origin).

### `!important` declarations

An `!important` at the end of a CSS declaration does not affect specificity but puts the declaration in a different [origin](https://web.dev/learn/css/the-cascade#origin), namely _Authored `!important`_.

In the following example, the specificity of `.my-class` is not relevant for the `!important` declaration to win.

```
.my-class {
  color: red !important;
  color: white;
}
```

When two declarations are `!important`, then the specificity comes in play again, as the origin step from the cascade was not able to determine the winner yet.

```
.branding {
  color: blue !important;
}

button {
  color: red !important;
}
```

## Specificity in context

When a complex or compound selector is used, each part of that selector adds up to the specificity. Consider this example HTML:

```
<a class="my-class another-class" href="#">A link</a>
```

This link has two classes on it. The rule in the following CSS has **a specificity of `(0,0,1)`**:

```
a {
  color: red;
}
```

If you reference one of the classes in the selector, it now has **a specificity of `(0,1,1)`**:

```
a.my-class {
  color: green;
}
```

Add the other class to the selector, it now has **a specificity of `(0,2,1)`**:

```
a.my-class.another-class {
  color: rebeccapurple;
}
```

Add the `href` attribute to the selector, it now has **a specificity of `(0,3,1)`**:

```
a.my-class.another-class[href] {
  color: goldenrod;
}
```

Finally,add a `:hover` pseudo-class to all of that, the selector ends up with **a specificity of `(0,4,1)`**:

```
a.my-class.another-class[href]:hover {
  color: lightgrey;
}
```

### Check your understanding

Test your knowledge of specificity scoring

Which of the following selectors has a specificity of **`(0,2,1)`**?

## Pragmatically increasing specificity

Say you have some CSS that looks like this:

```
.my-button {
  background: blue;
}

button[onclick] {
  background: grey;
}
```

With HTML that looks like this:

```
<button class="my-button" onclick="alert('hello')">Click me</button>
```

  CodePen Embed - Learn CSS - Matching specificity  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

The button has a grey background, because the second selector has **a specificity of `(0,1,1)`**. This is because it has one type selector (`button`), which is **`(0,0,1)`** and an attribute selector (`[onclick]`), which is **`(0,1,0)`**.

The previous rule—`.my-button`—equals **`(0,1,0)`** because it has one class selector, which is a lower specificity than `(0,1,1)`.

If you want to give this rule a boost, you can repeat the class selector like this:

```
.my-button.my-button {
  background: blue;
}

button[onclick] {
  background: grey;
}
```

  CodePen Embed - Learn CSS - Repetition boosts specificity  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Now, the button will have a blue background, because the new selector gets a specificity **`(0,2,0)`**

## A tie in specificity falls back to the next step in the cascade

Let's stay with the button example for now and switch the CSS around to this:

```
.my-button {
  background: blue;
}

[onclick] {
  background: grey;
}
```

The button has a grey background, because **both selectors have an identical specificity** of `(0,1,0)`.

  CodePen Embed - Learn CSS - Matching specificity  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

If you switch the rules in the source order, the button would then be blue.

```
[onclick] {
  background: grey;
}

.my-button {
  background: blue;
}
```

  CodePen Embed - Learn CSS - Matching specificity  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

This is because both selectors have the same specificity. In this case, the cascade falls back to [the order of appearance step](https://web.dev/learn/css/the-cascade#position_and_order_of_appearance).

## Resources

*   [CSS SpeciFISHity](http://specifishity.com/)
*   [Specificity Calculator](https://specificity.keegan.st/)
*   [MDN Specificity](https://developer.mozilla.org/docs/Web/CSS/Specificity)
*   [Specifics on CSS Specificity](https://css-tricks.com/specifics-on-css-specificity/)
*   [Another Specificity Calculator](https://polypane.app/css-specificity-calculator)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
