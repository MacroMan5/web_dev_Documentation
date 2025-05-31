# Optimize web fonts  |  web.dev

**Source URL:** [https://web.dev/learn/performance/optimize-web-fonts?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%2Foptimize-web-fonts](https://web.dev/learn/performance/optimize-web-fonts?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%2Foptimize-web-fonts)  
**Last Updated:** 2025-05-23T01:14:50.359Z  
**Extracted:** 2025-05-31 16:58:10

---

# Glitch

In the previous modules, you learned how to optimize of HTML, CSS, JavaScript, and media resources. In this module, discover some methods to optimize web fonts.

Web fonts can impact page performance at both load time and rendering time. Large font files can take a while to download and negatively affect [First Contentful Paint (FCP)](https://web.dev/articles/fcp), while the incorrect [`font-display` value](https://developer.mozilla.org/docs/Web/CSS/@font-face/font-display) could cause undesirable layout shifts that contribute to a page's [Cumulative Layout Shift (CLS)](https://web.dev/articles/cls).

Before optimizing web fonts can be discussed, knowing how they're discovered by the browser can be helpful, so that you can understand how CSS prevents the retrieval of unnecessary web fonts in certain situations.

## Discovery

A page's web fonts are defined in a style sheet using a `@font-face` declaration:

```
@font-face {
  font-family: "Open Sans";
  src: url("/fonts/OpenSans-Regular-webfont.woff2") format("woff2");
}
```

The preceding code snippet defines a `font-family` named `"Open Sans"`, and tells the browser where to find the respective web font resource. To conserve bandwidth, the browser does not download the web font until it is determined that the current page's layout needs it.

```
h1 {
  font-family: "Open Sans";
}
```

In the preceding CSS snippet, the browser downloads the `"Open Sans"` font file as it parses an `<h1>` element in the page's HTML.

### `preload`

If your `@font-face` declarations are defined in an external style sheet, the browser can only begin downloading them after it has downloaded the style sheet. This makes web fonts late-discovered resources—but there are ways to help the browser discover web fonts sooner.

You can initiate an early request for web font resources by using the `preload` directive. The `preload` directive makes web fonts discoverable early during page load, and the browser immediately begins downloading them without waiting for the style sheet to finish downloading and parsing. The `preload` directive does not wait until the font is needed on the page.

```
<!-- The `crossorigin` attribute is required for fonts—even
     self-hosted ones, as fonts are considered CORS resources. -->
<link rel="preload" as="font" href="/fonts/OpenSans-Regular-webfont.woff2" crossorigin>
```

### Inline `@font-face` declarations

You can make fonts discoverable earlier during page load by inlining render-blocking CSS—including the `@font-face` declarations—in the `<head>` of your HTML using the [`<style>` element](https://developer.mozilla.org/docs/Web/HTML/Element/style). In this case, the browser discovers web fonts earlier in the page load, as it does not need to wait for an external style sheet to download.

Inlining `@font-face` declarations has an advantage over using the `preload` hint, as the browser only downloads the fonts necessary to render the current page. This eliminates the risk of downloading unused fonts.

## Download

After discovering web fonts and ensuring they are needed by the current page's layout, the browser can download them. The number of web fonts, their encoding, and their file size can significantly affect how quickly a web font is downloaded and rendered by the browser.

### Self-host your web fonts

Web fonts can be served through third-party services, such as [Google Fonts](https://fonts.google.com/), or can be self-hosted on your origin. When using a third-party service, your web page needs to open a connection to the provider's domain before it can start downloading the needed web fonts. This can delay discovery and subsequent downloading of web fonts.

This overhead can be reduced using the `preconnect` resource hint. By using `preconnect`, you can tell the browser to open a connection to the cross-origin sooner than the browser ordinarily would:

```
<link rel="preconnect" href="https://fonts.googleapis.com">  
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```

The preceding HTML snippet hints the browser to establish a connection to `fonts.googleapis.com` and a [CORS](https://developer.mozilla.org/docs/Web/HTTP/CORS) connection to `fonts.gstatic.com`. Some font providers—such as Google Fonts—serve CSS and font resources from different origins.

You can eliminate the need for a third-party connection by self-hosting your web fonts. In most cases, self-hosting web fonts is faster than downloading them from a cross-origin. If you plan on self-hosting web fonts, check that your site is using a [Content Delivery Network (CDN)](https://web.dev/articles/content-delivery-networks), [HTTP/2](https://web.dev/articles/performance-http2) or HTTP/3, and sets the correct caching headers for the web fonts you need for your website.

### Use WOFF2—and WOFF2 only

[WOFF2](https://www.w3.org/TR/WOFF2/) enjoys [wide browser support](https://caniuse.com/woff2) and the best compression—up to 30% better than WOFF. The reduced file size leads to quicker download times. The WOFF2 format is often the only one needed for full compatibility across modern browsers.

### Subset your web fonts

Web fonts typically include a wide range of different [glyphs](https://en.wikipedia.org/wiki/Glyph), which are needed to represent the wide variety of characters used in different languages. If your page serves content in only one language—or uses a single alphabet—then you can reduce the size of your web fonts through subsetting. This often done by specifying a number—or a range of—[unicode code points](https://en.wikipedia.org/wiki/Code_point#In_Unicode).

A subset is a reduced set of the glyphs that were included in the original web font file. For example, instead of serving all glyphs, your page might serve a specific subset for Latin characters. Depending on the subset needed, removing glyphs can significantly reduce the size of a font file.

Some web font providers—such as Google Fonts—offer subsets automatically through the use of a query string parameter. For example, the `https://fonts.googleapis.com/css?family=Roboto&subset=latin` URL serves a style sheet with the Roboto web font that only use the Latin alphabet.

If you've decided to self-host your web fonts, the next step is to generate and host those subsets yourself using tools such as [glyphanger](https://github.com/zachleat/glyphhanger) or [subfont](https://github.com/Munter/subfont).

However, if you don't have the capacity to self-host your own web fonts, you can subset web fonts provided by Google Fonts by specifying an additional `text` query string parameter containing only the unicode code points necessary for your website. For example, if you have a display web font on your site that only needs a small number of characters needed for the phrase "Welcome", you can request that subset through Google Fonts through the following URL: `https://fonts.googleapis.com/css?family=Monoton&text=Welcome`. This can _significantly_ reduce the amount of web font data needed for a single typeface on your website, if such extreme subsetting can be useful on your website.

## Font rendering

After the browser has discovered and downloaded a web font, it can then be rendered. By default, the browser blocks the rendering of any text that uses a web font until the it's downloaded. You can adjust the browser's text rendering behavior, and configure what text should be shown—or not shown—until the web font has fully loaded using the [`font-display` CSS property](https://developer.mozilla.org/docs/Web/CSS/@font-face/font-display).

### `block`

The default value for `font-display` is `block`. With `block`, the browser blocks the rendering of any text that uses the specified web font. Different browsers behave slightly differently. Chromium and Firefox block rendering for up to a maximum of 3 seconds before using a fallback. Safari blocks indefinitely until the web font has loaded.

### `swap`

[`swap` is the most widely used `font-display` value](https://almanac.httparchive.org/en/2022/fonts#fig-13). `swap` does not block rendering, and shows the text immediately in a fallback before swapping in the specified web font. This lets you show your content immediately without waiting for the web font to download.

However, the downside of `swap` is that it causes a layout shift if the fallback web font and the web font specified in your CSS varies greatly in terms of line height, kerning, and other font metrics. This can affect your website's [CLS](https://web.dev/articles/cls) if you don't take care to use `preload` hint to load a web font resource as soon as possible, or if you don't consider other `font-display` values.

### `fallback`

The `fallback` value for `font-display` is something of a compromise between `block` and `swap`. Unlike `swap`, the browser blocks rendering of a font, but swap in fallback text only for a very short period of time. Unlike `block`, however, the blocking period is extremely short.

Using the `fallback` value can work well on fast networks where, if the web font downloads quickly, the web font is the typeface used immediately on the page's initial rendering. However, if networks are slow, the fallback text is seen first after the blocking period elapses, and then swapped out when the web font arrives.

### `optional`

`optional` is the most stringent `font-display` value, and only uses the web font resource if it downloads within 100 milliseconds. If a web font takes longer than that to load, it isn't used on the page, and the browser uses the fallback typeface for the current navigation while the web font is downloaded in the background and placed in the browser cache.

As a result, subsequent page navigations can use the web font immediately, since it's already downloaded. `font-display: optional` avoids the layout shift seen with `swap`, but some users don't see the web font if it arrives too late on the initial page navigation.

### Font demos

## Test your knowledge

When does the browser download a web font resource (assuming it isn't fetched with a `preload` directive)?

When the page's CSSOM is built and it is determined the web font is needed for the current layout.

As soon as the reference to it is discovered in a style sheet.

What is the only (and most efficient) format necessary to serve web fonts to all modern browsers?

## Up next: Code-split JavaScript

With an understanding of font optimization under your belt, you can now move onto the next module, which covers a topic that has a high potential to improve initial page load speed for your users, and that is to [defer the loading of JavaScript through code splitting](https://web.dev/learn/performance/code-split-javascript). By doing so, you can keep bandwidth and CPU contention as low as possible during the startup phase of a page, a period of time in which users are quite likely to interact with it.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
