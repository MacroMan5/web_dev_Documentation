# Styling form controls  |  web.dev

**Source URL:** [https://web.dev/learn/forms/styling-form-controls?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fstyling-form-controls](https://web.dev/learn/forms/styling-form-controls?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fstyling-form-controls)  
**Last Updated:** 2025-05-23T01:00:40.380Z  
**Extracted:** 2025-05-31 16:58:10

---

# Styling form controls | web.dev

Styling form controls

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

In this module you learn how to style form controls, and how to match your other site styles.

## Help users select an option

### The `<select>` element

The default styles of a `<select>` element don't look great, and the appearance is inconsistent between browsers.

  CodePen Embed - Learn forms – unstyled select element  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

First, let's change the arrows.

```
select {
    -moz-appearance: none;
    -webkit-appearance: none;
    appearance: none;
    background-color: #fff;
    background-image: url(arrow.png);
    background-repeat: no-repeat;
    background-position: right .7em top 50%, 0 0;
    background-size: .65em auto;
}
```

To remove the default arrows of a `<select>` element, use the CSS [`appearance`](https://developer.mozilla.org/docs/Web/CSS/appearance) property. To show the arrow of your choice, define the arrow as a `background`.

You should also change the `font-size` to at least `1rem` (which for most browsers has a default value of 16px) for your `<select>` element. Doing so will prevent a page zoom on iOS Safari when the form control is focused.

You can, of course, also change the element colors to match your brand colors. After adding some more styles for spacing, `:hover`, and `:focus`, the appearance of the `<select>` element is now consistent between browsers.

See this in the following demo from [Styling a Select Like It’s 2019](https://www.filamentgroup.com/lab/select-css.html)

  CodePen Embed - Learn forms – styled select element  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

What about the `<option>` element? The `<option>` element is a so-called [replaced element](https://developer.mozilla.org/docs/Web/CSS/Replaced_element) whose representation is outside the scope of CSS. As of this writing, you can't style the `<option>` element.

### Checkboxes and Radio buttons

The appearance of `<input type="checkbox">` and `<input type="radio">` varies across browsers.

  CodePen Embed - Learn forms – unstyled checkbox and radio element  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

Open the [demo](https://codepen.io/web-dot-dev/pen/74d28931d0c0e9aacc89f62380f365e4) on various browsers to see the difference. Let's see how to make sure that checkboxes and radio buttons match your brand and look the same cross-browser.

In the past, developers could not style `<input type="checkbox">` and `<input type="radio">` controls directly. [Checkboxes and radio buttons can be styled via their pseudo elements](https://www.scottohara.me/blog/2021/09/24/custom-radio-checkbox-again.html), now. Or the following replacement technique can be used to create custom styles for these elements.

First, hide the default checkbox and radio button visually.

```
input[type="radio"],
input[type="checkbox"] {
   position: absolute;
   opacity: 0;
}
```

It's important to use `position: absolute` in combination with `opacity: 0` instead of `display: none` or `visibility: hidden` so that the controls are only visually hidden. This will ensure they are still exposed by the browser's [accessibility tree](https://web.dev/articles/the-accessibility-tree). Note that further styling may be needed to ensure that the visually hidden form controls remain positioned "on top" of their replacement elements. Doing so will help ensure that hovering over one of these elements, when a screen reader is on, or when using touch devices with screen readers enabled, the visually hidden controls will be discoverable if exploring by touch, and the screen reader's visible focus indicator will generally appear in the location the controls are rendered on screen.

To show your custom checkboxes and radio buttons, you have different options. You use the `::before` CSS pseudo-element and the CSS `background` property, or use inline SVG images.

```
input[type="radio"] + label::before {
  content: "";
  width: 1em;
  height: 1em;
  border: 1px solid black;
  display: inline-block;
  border-radius: 50%;
  margin-inline-end: 0.5em;
}

input[type="radio"]:checked + label::before {
  background: black;
}
```

There are a lot of possibilities with CSS to ensure checkboxes and radio buttons match your brand styles.

  CodePen Embed - Learn forms – styled checkbox and radio element  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

Learn more about [styling `<input type="checkbox">`, and `<input type="radio">`](https://www.sarasoueidan.com/blog/inclusively-hiding-and-styling-checkboxes-and-radio-buttons/) and [custom checkbox styles](https://moderncss.dev/pure-css-custom-checkbox-style/).

## How to use your site's colors for form controls

Do you want to bring your site styles to form controls with one line of code? You can use the [`accent-color`](https://web.dev/articles/accent-color) CSS property to achieve this.

```
checkbox {
  accent-color: orange;
}
```

### Check your understanding

Test your knowledge of styling form controls

How can you remove platform-native styling of form controls?

Using `revert: appearance;`.

Using `appearance: revert;`.

## Resources

*   [Accent color](https://web.dev/articles/accent-color)
*   [Styling the `<select>` element](https://www.filamentgroup.com/lab/select-css.html)
*   [The Accessibility of Styled Form Controls](https://scottaohara.github.io/a11y_styled_form_controls/)
*   [Open UI](https://open-ui.org/)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
