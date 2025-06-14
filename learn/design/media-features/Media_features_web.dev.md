# Media features  |  web.dev

**Source URL:** [https://web.dev/learn/design/media-features?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%2Fmedia-features](https://web.dev/learn/design/media-features?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%2Fmedia-features)  
**Last Updated:** 2025-05-23T00:55:16.853Z  
**Extracted:** 2025-05-31 16:58:10

---

# Media features  |  web.dev

A round-up of all the ways that media features let you respond to devices and preferences.

Responsive design wouldn't be possible without media queries. Before media queries there was no way of knowing what kind of device people were using to visit your website. Designers had to make assumptions. Those assumptions were encoded into fixed-width designs or liquid layouts.

That all changed with the introduction of [media queries](https://web.dev/learn/design/media-queries). For the first time designers could meet people halfway. Designers could adjust their layouts to respond to people's devices.

Remember, a media query comprises an optional media type and a mandatory media feature. There hasn't been much change in media types over the years. There are still just four possible values:

```
@media all
@media screen
@media print
@media speech
```

[Media features](https://developer.mozilla.org/docs/Web/CSS/@media#media_features), on the other hand, have expanded greatly. Designers now can meet users beyond halfway, adapting designs to fit far more than just screen size.

## Viewport dimensions

By far the most popular media queries on the web are the ones dealing with viewport width. But even here, you're presented with a choice. You can use the `max-width` media feature to apply styles below a certain width, or you can use the `min-width` media feature to apply styles above a certain width.

```
main {
  display: grid;
  grid-template-columns: 2fr 1fr;
}
@media (max-width: 45em) {
  main {
    display: block;
  }
}
```
```
@media (min-width: 45em) {
  main {
    display: grid;
    grid-template-columns: 2fr 1fr;
  }
}
```

Personally, I like to use `min-width`. I apply layout styles in an additive way. I introduce new layout rules at each breakpoint instead of undoing previous rules.

This additive approach also works for height. Using `min-height` you can introduce more rules as more viewport height becomes available. For example, you might have a header element that you want to anchor to the top of the browser window if there's enough vertical space.

```
@media (min-height: 30em) {
  header {
    position: fixed;
  }
}
```

  CodePen Embed - Sticky header  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

But you can use the `max-height` media feature if you prefer. Here, the header is anchored by default, but the stickiness is removed if there isn't enough vertical space.

```
header {
  position: fixed;
}
@media (max-height: 30em) {
  header {
    position: static;
  }
}
```

Choosing between `min-` and `max-` prefixes doesn't just apply to [`width`](https://developer.mozilla.org/docs/Web/CSS/@media/width) and [`height`](https://developer.mozilla.org/docs/Web/CSS/@media/height). The [`aspect-ratio`](https://developer.mozilla.org/docs/Web/CSS/@media/aspect-ratio) media feature offers the same choice. It also offers an unprefixed version if you want to apply styles at an exact ratio of width to height.

```
@media (min-aspect-ratio: 16/9) {
  // The ratio of width to height is at least 16 by 9.
}
@media (max-aspect-ratio: 16/9) {
  // The ratio of width to height is less than 16 by 9.
}
@media (aspect-ratio: 16/9) {
  // The ratio of width to height is exactly 16 by 9.
}
```

Providing different styles for different aspect ratios could quickly get out of hand. If you don't need that fine-grained level of control, the [`orientation`](https://developer.mozilla.org/docs/Web/CSS/@media/orientation) media feature might better suit your needs. It has two possible values: `portrait` or `landscape`.

```
@media (orientation: portrait) {
  // The width is less than the height.
}
@media (orientation: landscape) {
  // The width is greater than the height.
}
```

  CodePen Embed - Orientation media query  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Even though the terms "portrait" and "landscape" are most often used to refer to the orientation of mobile devices, the `orientation` media feature isn't device-specific. A full-screen browser window on a typical laptop will have an `orientation` value of `landscape`.

## Displays

Different displays have different pixel densities, measured in `dpi`, dots per inch. You can adjust your styles for different pixel densities using the [`resolution`](https://developer.mozilla.org/docs/Web/CSS/@media/resolution) media feature. Like `aspect-ratio`, `resolution` comes in three varieties: minimum, maximum, and exact.

```
@media (min-resolution: 300dpi) {
  // The display has a pixel density of at least 300 dots per inch.
}
@media (max-resolution: 300dpi) {
  // The display has a pixel density less than 300 dots per inch.
}
@media (resolution: 300dpi) {
  // The display has a pixel density of exactly 300 dots per inch.
}
```

You may never need to use any `resolution` media queries. Pixel density is usually only an issue for images, and [responsive images](https://web.dev/learn/design/responsive-images) are a way of dealing with pixel density directly in HTML.

On the other hand, CSS is where you define your animations and transitions. You can adjust those animations and transitions to respond to different refresh rates using the [`update`](https://developer.mozilla.org/docs/Web/CSS/@media/update-frequency) media feature. This media feature reports one of three values: `none`, `slow`, and `fast`.

An `update` value of `none` means there's no refresh rate. A printed page, for example, can't be updated.

An `update` value of `slow` means the display can't refresh quickly. An e-ink display is one example of a screen with a slow refresh rate.

An `update` value of `fast` means the display refreshes fast enough to handle animations and transitions.

```
@media (update: fast) {
  a {
    transition-duration: 0.4s;
    transition-property: transform;
  }
  a:hover {
    transform: scale(150%);
  }
}
```

Not all aspects of the display are related to hardware capabilities. In [the module on theming](https://web.dev/learn/design/theming), you saw how to define properties in a [web app manifest](https://web.dev/articles/add-manifest) file. One of those properties is called `display`, and you can give it a value of `fullscreen`, `standalone`, `minimum-ui`, or `browser`. The corresponding [`display-mode`](https://developer.mozilla.org/docs/Web/CSS/@media/display-mode) media feature allows you to tailor your styles for these different options.

Let's say you've provided a `display` value of `standalone` in your web app manifest. If someone adds your site to their home screen, the site will launch without any browser interface. You might decide to display a back button for those users.

```
button.back {
  display: none;
}
@media (display-mode: standalone) {
  button.back {
     display: inline;
  }
}
```

## Color

There are numerous media features for querying the color capabilities of a device. If you want to adjust your styles for any display that only outputs shades of grey, you can use the [`monochrome`](https://developer.mozilla.org/docs/Web/CSS/@media/monochrome) media feature without any value.

```
@media (monochrome) {
  body {
    color: black;
    background-color: white;
  }
}
```

There's a corresponding [`color`](https://developer.mozilla.org/docs/Web/CSS/@media/color) media feature.

```
@media (color) {
  body {
    color: maroon;
    background-color: linen;
  }
}
```

For color screens, you can write queries with the media features [`color-gamut`](https://developer.mozilla.org/docs/Web/CSS/@media/color-gamut), [`color-index`](https://developer.mozilla.org/docs/Web/CSS/@media/color-index), or [`dynamic-range`](https://www.w3.org/TR/mediaqueries-5/#dynamic-range). All of them report specific details about the color capabilities of the screen.

In this example, color values update in response to the `dynamic-range` media feature, which reports the combination of maximum brightness, color depth, and contrast ratio of the display. The possible values are `standard` or `high`. A high-definition screen that reports a `dynamic-range` value of `high` is given a different color space using the new CSS `color()` function.

```
.neon-red {
  color: hsl(355 100% 95%);
}
@media (dynamic-range: high) {
  .neon-red {
    color: color(display-p3 1 0 0);
  }
}
```

  CodePen Embed - HD CSS Beat Saber Logo Glow  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

## Interaction

Media features can also report the kind of input mechanism used to interact with your site: `hover`, `any-hover`, `pointer`, and `any-pointer`. See [the module on interaction](https://web.dev/learn/design/interaction) for more details.

## Preferences

There are a range of media queries that allow you to respond to user preferences: `prefers-color-scheme`, `prefers-contrast`, and `prefers-reduced-motion`. See the modules on [theming](https://web.dev/learn/design/theming) and [accessibility](https://web.dev/learn/design/accessibility) for more details.

You can combine media features in one media query. You could scope your animation styles so that they're only applied if the device has a fast refresh rate and the user hasn't expressed a preference for reduced motion.

```
@media (update: fast) and (prefers-reduced-motion: no-preference) {
  a {
    transition-duration: 0.4s;
    transition-property: transform;
  }
  a:hover {
    transform: scale(150%);
  }
}
```

There are more media features on the way.

The [`forced-colors`](https://developer.mozilla.org/docs/Web/CSS/@media/forced-colors) and [`inverted-colors`](https://developer.mozilla.org/docs/Web/CSS/@media/inverted-colors) media features will report whether a device is using a restricted or an inverted color palette.

A [`scripting`](https://developer.mozilla.org/docs/Web/CSS/@media/scripting) media feature will allow you to adjust your CSS based on the availability of JavaScript.

A media feature called [`prefers-reduced-data`](https://developer.mozilla.org/docs/Web/CSS/@media/prefers-reduced-data) will allow users to specify that they're on a metered connection so you can send smaller or fewer assets.

Other proposals are still being formulated. In the next and final module, you'll learn about a proposal for a media feature that handles different screen configurations.

### Check your understanding

Test your knowledge of media features

A media query can check for a device at a specific width like `@media (width: 1024px)`?

A media query can check for a device at a specific `aspect-ratio` like `@media (aspect-ratio: 4/3)`?

Which are valid color media queries?

`@media (min-color-index: 15000)`

`@media (dynamic-range: high)`

`@media (color-gamut: srgb)`

Which of the following user preference media queries are valid?

`@media (prefers-colors: high-definition)`

`@media (prefers-contrast: more)`

`@media (prefers-site-speed: fast)`

`@media (prefers-reduced-motion: reduce)`

`@media (prefers-color-scheme: dark)`

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
