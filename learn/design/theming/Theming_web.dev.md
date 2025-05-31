# Theming  |  web.dev

**Source URL:** [https://web.dev/learn/design/theming?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%2Ftheming](https://web.dev/learn/design/theming?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%2Ftheming)  
**Last Updated:** 2025-05-23T00:54:54.536Z  
**Extracted:** 2025-05-31 16:58:10

---

# Theming  |  web.dev

Even branding can be responsive. You can adjust the presentation of your website to match the user's preference. But first, here's how to extend your website's branding to include the browser itself.

## Customize the browser interface

Some browsers allow you to suggest a theme color based on your website's palette. The browser's interface adapts to your suggested color. Add the color in a `meta` element named `theme-color` in the `head` of your pages.

```
<meta name="theme-color" content="#00D494">
```

![Clearleft dot com.](https://web.dev/static/learn/design/theming/image/clearleft-dot-com-fc330772c30d.png) ![Resilient Web Design dot com.](https://web.dev/static/learn/design/theming/image/resilient-web-design-dot-79ec7ad52532.png) ![The Session dot org.](https://web.dev/static/learn/design/theming/image/the-session-dot-org-138442c2e4689.png)

Three websites are viewed in the Safari browser. Each one has its own theme color that extends into the browser interface.

You can update the value of `theme-color` using JavaScript. But use this power wisely. It can be overwhelming for users if their browser's color scheme changes too often. Think about subtle ways to adjust the theme color. If the changes are too jarring, users will leave in annoyance.

You can also specify a theme color in a [web app manifest](https://developer.mozilla.org/docs/Web/Manifest) file. This is a JSON file with metadata about your website.

Link to the manifest file from the `head` of your documents. Use a `link` element with a `rel` value of `manifest`.

```
<link rel="manifest" href="/manifest.json">
```

In the manifest file, list your metadata using key/value pairs.

```
{
  "short_name": "Clearleft",
  "name": "Clearleft design agency",
  "start_url": "/",
  "background_color": "#00D494",
  "theme_color": "#00D494",
  "display": "standalone"
}
```

If a visitor decides to add your website to their home screen, the browser will use the information in your manifest file to display an appropriate shortcut.

## Provide a dark mode

Many operating systems allow users to specify a preference for a light or a dark color palette, which is a good idea to optimize your site to your user's theme preferences. You can access this preference in a media feature called `prefers-color-scheme`.

```
@media (prefers-color-scheme: dark) {
  // Styles for a dark theme.
}
```

  CodePen Embed - Dark mode  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

Specify theme colors with the `prefers-color-scheme` media feature within the `meta` element.

```
<meta name="theme-color" content="#ffffff" media="(prefers-color-scheme: light)">
<meta name="theme-color" content="#000000" media="(prefers-color-scheme: dark)">
```

You can also use the `prefers-color-scheme` media feature inside SVG. If you use an SVG file for your favicon, it can be adjusted for dark mode. [Thomas Steiner](https://web.dev/authors/thomassteiner) wrote about [`prefers-color-scheme` in SVG favicons for dark mode icons](https://blog.tomayac.com/2019/09/21/prefers-color-scheme-in-svg-favicons-for-dark-mode-icons/).

## Theming with custom properties

If you use the same color values in multiple places throughout your CSS, it could be quite tedious to repeat all your selectors within a `prefers-color-scheme` media query.

```
body {
  background-color: white;
  color: black;
}
input {
  background-color: white;
  color: black;
  border-color: black;
}
button {
  background-color: black;
  color: white;
}
@media (prefers-color-scheme: dark) {
  body {
    background-color: black;
    color: white;
  }
  input {
    background-color: black;
    color: white;
    border-color: white;
  }
  button {
    background-color: white;
    color: black;
  }
}
```

Use CSS custom properties to store your color values. Custom properties work like variables in a programming language. You can update the value of a variable without updating its name.

If you update the values of your custom properties within a `prefers-color-scheme` media query, you won't have to write all your selectors twice.

```
html {
  --page-color: white;
  --ink-color: black;
}
@media (prefers-color-scheme: dark) {
  html {
    --page-color: black;
    --ink-color: white;
  }
}
body {
  background-color: var(--page-color);
  color: var(--ink-color);
}
input {
  background-color: var(--page-color);
  color: var(--ink-color);
  border-color: var(--ink-color);
}
button {
  background-color: var(--ink-color);
  color: var(--page-color);
}
```

  CodePen Embed - Dark mode with custom properties  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

See [building a color scheme](https://web.dev/articles/building/a-color-scheme) for more advanced examples of theming with custom properties.

## Images

If you are using SVGs in your HTML, you can apply custom properties there too.

```
svg {
  stroke: var(--ink-color);
  fill: var(--page-color);
}
```

Now your icons will change their colors along with the other elements on your page.

If you want to tone down the brightness of your photographic images when displayed in dark mode, you can apply a filter in CSS.

```
@media (prefers-color-scheme: dark) {
  img {
    filter: brightness(.8) contrast(1.2);
  }
}
```

  CodePen Embed - Images in dark mode  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

![Three photographs at normal brightness.](https://web.dev/static/learn/design/theming/image/three-photographs-normal-e7cfaee065a3.png) ![Three photographs with slightly less brightness.](https://web.dev/static/learn/design/theming/image/three-photographs-slight-6ca40f542a4e9.png)

The effect is subtle, but you can tone down the brightness of images in dark mode.

For some images, you might want to swap them out completely in dark mode. For example, you might want to show a map with a darker color scheme. Use the `<picture>` element containing a `<source>` element with the `prefers-color-scheme` media query.

```
<picture>
  <source srcset="darkimage.png" media="(prefers-color-scheme: dark)">
  <img src="lightimage.png" alt="A description of the image.">
</picture>
```

  CodePen Embed - Image switching in dark mode  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

![Two maps of Broolyn, one using light colors and the other using dark colors.](https://web.dev/static/learn/design/theming/image/two-maps-broolyn-using-5ab9d5d846e67.png)

Two versions of the same map, one for light mode and one for dark mode.

## Forms

Browsers provide a default color palette for form fields. Let the browser know that your site offers both a dark and a light mode. That way, the browser can provide the appropriate default styling for forms.

Add this to your CSS:

```
html {
  color-scheme: light;
}
@media (prefers-color-scheme: dark) {
  html {
    color-scheme: dark;
  }
}
```

You can also use HTML. Add this in the `head` of your documents:

```
<meta name="supported-color-schemes" content="light dark">
```

  CodePen Embed - Forms in dark mode  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

Use the [`accent-color`](https://web.dev/articles/accent-color) property in CSS to style checkboxes, radio buttons, and some other form fields.

```
html {
  accent-color: red;
}
```

It's common for dark themes to have subdued brand colors. You can update the `accent-color` value for dark mode.

```
html {
  accent-color: red;
}
@media (prefers-color-scheme: dark) {
  html {
    accent-color: pink;
  }
}
```

It makes sense to use a custom property for this so you can keep all your color declarations in one place.

```
html {
  color-scheme: light;
  --page-color: white;
  --ink-color: black;
  --highlight-color: red;
}
@media (prefers-color-scheme: dark) {
  html {
    color-scheme: dark;
    --page-color: black;
    --ink-color: white;
    --highlight-color: pink;
  }
}
html {
  accent-color: var(--highlight-color);
}
body {
  background-color: var(--page-color);
  color: var(--ink-color);
}
```

  CodePen Embed - Accent color in dark mode  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

Providing a dark mode is just one example of adapting your site to suit your user's preferences. Next you'll learn how to make your site adaptable to all sorts of [accessibility](https://web.dev/learn/design/accessibility) considerations.

### Check your understanding

Test your knowledge on theming

To provide theme colors that impact the browser outside of the webpage, use:

A 'theme-color' `<meta>` tag

To hook into a user's system preference regarding a light or dark theme, use:

The `(prefers-color-scheme)` media query

So you support dark theme, but all the form inputs are still light themed. What can you do?

Write a bunch of CSS to change all the defaults of the input.

Add `<meta name="supported-color-schemes" content="light dark">` to your HTML `<head>` tag.

Add `html { color-scheme: light dark; }` to your CSS.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
