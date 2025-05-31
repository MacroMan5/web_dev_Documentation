# Icons  |  web.dev

**Source URL:** [https://web.dev/learn/design/icons?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%2Ficons](https://web.dev/learn/design/icons?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%2Ficons)  
**Last Updated:** 2025-05-23T00:54:50.462Z  
**Extracted:** 2025-05-31 16:58:10

---

# Icons  |  web.dev

Most images are part of your content, but icons are part of your user interface. They should scale and adapt in the same way that the text of your UI scales and adapts.

## Scalable Vector Graphics

When it comes to photographic imagery, there are lots of choices for the image format: JPG, WebP, and AVIF. For non-photographic imagery, you have a choice between the Portable Network Graphics (PNG) format and the Scalable Vector Graphics (SVG) format.

Both PNGs and SVGs are good at dealing with areas of flat color, and they both allow your images to have transparent backgrounds. If you use a PNG you'll probably need to make multiple versions of your image in different sizes and use the `srcset` attribute on your `img` element to [make the image responsive](https://web.dev/learn/design/responsive-images). If you use an SVG, it's responsive by default.

PNGs (and JPGs, WebP, and AVIF) are bitmap images. Bitmap images store information as pixels. In an SVG, information is stored as drawing instructions. When the browser reads the SVG file the instructions are converted into pixels. Best of all, these instructions are relative. Regardless of the dimensions you use to describe lines and shapes, everything renders at just the right crispness. Instead of creating multiple SVGs of different sizes you can make one SVG that will work at all sizes. There's no need to use the `srcset` attribute.

```
<img src="image.svg" alt="A description of the image." width="25" height="25">
<img src="image.svg" alt="A description of the image." width="250" height="250">
```

  CodePen Embed - Sizing SVG images  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

XML is used to write the instructions in an SVG file. This is a markup language, like HTML.

```
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE svg>
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" viewBox="-21 -21 42 42" width="100" height="100">
  <title>Smiling face</title>
  <circle r="20" fill="yellow" stroke="black"/>
  <ellipse rx="2.5" ry="4" cx="-6" cy="-7" fill="black"/>
  <ellipse rx="2.5" ry="4" cx="6" cy="-7" fill="black"/>
  <path stroke="black" d="M -12,5 A 13.5,13.5,0 0,0 12,5 A 13,13,0 0,1 -12,5"/>
</svg>
```

![Smiley face.](https://web.dev/static/learn/design/icons/image/smiley-face-c6edfc71214c.svg)

You can even put SVG inside HTML.

```
<figure>
  <svg version="1.1" xmlns="http://www.w3.org/2000/svg" viewBox="-21 -21 42 42" width="100" height="100">
    <title>Smiling face</title>
    <circle r="20" fill="yellow" stroke="black"/>
    <ellipse rx="2.5" ry="4" cx="-6" cy="-7" fill="black"/>
    <ellipse rx="2.5" ry="4" cx="6" cy="-7" fill="black"/>
    <path stroke="black" d="M -12,5 A 13.5,13.5,0 0,0 12,5 A 13,13,0 0,1 -12,5"/>
  </svg>
  <figcaption>
  A description of the image.
  </figcaption>
</figure>
```

If you embed an SVG like that, that's one less request that the browser needs to make. There'll be no wait for the image to download because it arrives with the HTML …_in_ the HTML! Also, as you'll soon find out, embedding SVGs like this gives you more control over styling them too.

## Icons and text

Icon images often feature simple shapes on a transparent background. SVG is ideal for icons.

If you have a button or a link with text and an icon inside it, the icon is presentational. It's the text that matters. When using an `img` element, an empty `alt` attribute indicates that the image is presentational.

```
<button>
<img src="hamburger.svg" alt="" width="16" height="16">
Menu
</button>
```

  CodePen Embed - Icon and text  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Because CSS is for presentation, you could put the icon in your CSS as a background image.

```
<button class="menu">
Menu
</button>
```
```
.menu {
  background-image: url(hamburger.svg);
  background-position: 0.5em;
  background-repeat: no-repeat;
  background-size: 1em;
  padding-inline-start: 2em;
}
```

  CodePen Embed - Background icon and text  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

If you put the SVG inside your HTML, use the `aria-hidden` attribute to hide it from assistive technology.

```
<button class="menu">
  <svg aria-hidden="true" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 80" width="16" height="16">
    <rect width="100" height="20" />
    <rect y="30" width="100" height="20"/>
    <rect y="60" width="100" height="20"/>
  </svg>
  Menu
</button>
```

  CodePen Embed - Embedded icon and text  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Standalone icons

Use text inside your buttons and links if you want their purpose to be clear. You can use an icon without any text but don't assume that everyone understands the meaning of a particular icon. When in doubt, test with real users.

If you decide to use an icon without any accompanying text, the icon is no longer presentational. A background image in CSS is not an appropriate way to display the icon. The icon needs to be given an accessible name in HTML.

If you use an `img` element, the icon gets its accessible name from the `alt` attribute.

```
<button>
<img src="hamburger.svg" alt="Menu" width="16" height="16">
</button>
```

  CodePen Embed - Standalone icon  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Another option is to put the accessible name on the link or button itself and declare that the image is presentational. Use the `aria-label` attribute to provide the accessible name.

```
<button aria-label="Menu">
<img src="hamburger.svg" alt="" width="16" height="16">
</button>
```

  CodePen Embed - Standalone icon with aria-label  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

If you put the SVG inside your HTML, use the `aria-label` attribute on the link or button to give it an accessible name and use the `aria-hidden` attribute on the icon.

```
<button aria-label="Menu">
  <svg aria-hidden="true" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 80" width="16" height="16">
    <rect width="100" height="20" />
    <rect y="30" width="100" height="20"/>
    <rect y="60" width="100" height="20"/>
  </svg>
</button>
```

  CodePen Embed - Standalone embedded icon with aria-label  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Styling icons

If you embed your SVG icons directly in your HTML you can style parts of them just like any other element in your page. You can't do that if you use an `img` element to display your icons.

In the following example, the `rect` elements inside the SVG have a `fill` value of `blue` to match the styles for the button's text.

```
button {
 color: blue;
}
button rect {
  fill: blue;
}
```

You can apply `hover` and `focus` styles too.

```
button:hover,
button:focus {
  color: red;
}
button:hover rect,
button:focus rect {
  fill: red;
}
```

  CodePen Embed - Embedded icon and text with hover  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Resources

*   If you need to style SVGs that are background images in your CSS, read Una's article on [colorizing SVG backgrounds](https://css-tricks.com/solved-with-css-colorizing-svg-backgrounds/).
*   Sara Soueidan has written about [accessible icon buttons](https://www.sarasoueidan.com/blog/accessible-icon-buttons/).
*   Scott O'Hara has written about [contextually marking up accessible images and SVGs](https://www.scottohara.me/blog/2019/05/22/contextual-images-svgs-and-a11y.html).
*   If you're using a graphic design tool to export SVGs, use [SVGOMG](https://jakearchibald.github.io/svgomg/) to optimize the output.

Icons are an important part of your site's branding. Next you'll find out how to make other aspects of your branding responsive through the power of [theming](https://web.dev/learn/design/theming).

### Check your understanding

Test your knowledge of icons

SVG can handle any pixel density with one single file or `<svg>` code block.

SVG code that's directly in the HTML has which advantages?

Light or dark themed without a new asset.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
