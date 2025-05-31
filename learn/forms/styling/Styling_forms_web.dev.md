# Styling forms  |  web.dev

**Source URL:** [https://web.dev/learn/forms/styling?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fstyling](https://web.dev/learn/forms/styling?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fstyling)  
**Last Updated:** 2025-05-23T01:00:31.963Z  
**Extracted:** 2025-05-31 16:58:10

---

# Styling forms  |  web.dev

Styling forms

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

## Help users use your form with their preferred browser

To ensure that your form is accessible to as many people as possible, use the elements built for the job: `<input>`, `<textarea>`, `<select>`, and `<button>`. This is the baseline for a usable form.

  CodePen Embed - Learn forms – unstyled  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

The default browser styles don't look great! Let's change that.

## Ensure form controls are readable for everyone

The default font size for form controls in most browsers is too small. To ensure your form controls are readable, change the font size with CSS:

  CodePen Embed - Learn forms – styling: font  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

Increase the `font-size` and `line-height` to improve readability.

```
.form-element {
  font-size: 1.3rem;
  line-height: 1.2;
}
```

## Help users navigate through your form

As a next step, change the layout of your form, and increase the spacing of form elements, to help users understand which elements belong together.

  CodePen Embed - Learn forms – styling: layout  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

The `margin` CSS property increases space between elements, and the `padding` property increases space around the element's content.

For the general layout, use [Flexbox](https://web.dev/learn/css/flexbox) or [Grid](https://web.dev/learn/css/grid). Learn more about [CSS layout methods](https://web.dev/learn/css/layout).

## Ensure form controls look like form controls

Make it easy for people to fill out your form by using well-understood styles for your form controls. For example, style `<input>` elements with a solid border.

  CodePen Embed - Learn forms – styling: border  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

```
input,
textarea {
  border: 1px solid;
}
```

## Help users submit your form

Consider using a `background` for your `<button>` to match your site style, and override or remove the default `border` styles.

  CodePen Embed - Learn forms – styling: button  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

## Help users understand the current state

Browsers apply a default style for `:focus`. You can override the styles for `:focus` to match the color to your brand.

```
button:focus {
    outline: 4px solid green;
}
```

### Check your understanding

Test your knowledge of styling forms

Why should you use relative units for `font-size`?

To ensure the size responds to dark mode.

To ensure the size responds to the previous element.

To ensure the size responds to media queries.

To ensure the size responds to user preference.

How can you increase spacing between form controls?

Using the `padding` CSS property.

Using the `spacer` CSS property.

Using the `boundary` CSS property.

Using the `margin` CSS property.

## Resources

*   [Learn CSS](https://web.dev/learn/css)
*   [CSS layout methods](https://web.dev/learn/css/layout)
*   [Designing focus indicators](https://www.sarasoueidan.com/blog/focus-indicators/)
*   [Reverting the default style of a `<button>`](https://archive.hankchizljaw.com/wrote/introducing-the-button-element/#heading-oh-these-are-hard-to-style-though).

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
