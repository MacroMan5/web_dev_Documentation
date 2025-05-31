# Optimize resource loading  |  web.dev

**Source URL:** [https://web.dev/learn/performance/optimize-resource-loading?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%2Foptimize-resource-loading](https://web.dev/learn/performance/optimize-resource-loading?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%2Foptimize-resource-loading)  
**Last Updated:** 2025-05-23T01:13:53.061Z  
**Extracted:** 2025-05-31 16:58:10

---

# Glitch

In the previous module, [some theory behind the critical rendering path](https://web.dev/learn/performance/understanding-the-critical-path) was explored, and how render-blocking and parser-blocking resources can delay a page's initial rendering. Now that you understand some of the theory behind this, you're ready to learn some techniques for optimizing the critical rendering path.

As a page loads, many resources are referenced within its HTML that provide a page with its appearance and layout through CSS, as well as its interactivity through JavaScript. In this module, a number of important concepts related to these resources and how they affect a page's load time are covered.

## Render blocking

As was discussed in the [previous module](https://web.dev/learn/performance/understanding-the-critical-path), CSS is a [render-blocking](https://web.dev/articles/critical-rendering-path/render-blocking-css) resource, as it blocks the browser from rendering any content until the [CSS Object Model (CSSOM)](https://developer.mozilla.org/docs/Web/API/CSS_Object_Model) is constructed. The browser blocks rendering to prevent a [Flash of Unstyled Content (FOUC)](https://en.wikipedia.org/wiki/Flash_of_unstyled_content), which is undesirable from a user experience standpoint.

 

In the preceding video, there is a brief FOUC where you can see the page without any styling. Subsequently, all styles are applied once the page's CSS has finished loading from the network, and the unstyled version of the page is immediately replaced with the styled version.

Generally speaking, a FOUC is something you don't normally see, but the concept is important to understand so that you know _why_ the browser blocks rendering of the page until CSS is downloaded and applied to the page. Render blocking isn't necessarily undesirable, but you do want to minimize how long it lasts by keeping your CSS optimized.

## Parser blocking

A [parser-blocking](https://web.dev/articles/critical-rendering-path/adding-interactivity-with-javascript) resource interrupts the HTML parser, such as a `<script>` element without `async` or `defer` attributes. When the parser encounters a `<script>` element, the browser needs to evaluate and execute the script before proceeding with parsing the rest of the HTML. This is by design, as scripts may modify or access the DOM during a time while it is still being constructed.

```
<!-- This is a parser-blocking script: -->
<script src="/script.js"></script>
```

When using external JavaScript files (without `async` or `defer`), the parser is blocked from when the file is discovered until it is downloaded, parsed, and executed. When using inline JavaScript, the parser is similarly blocked until the inline script is parsed and executed.

## The preload scanner

The [preload scanner](https://web.dev/articles/preload-scanner) is a browser optimization in the form of a secondary HTML parser that scans the raw HTML response to find and speculatively fetch resources before the primary HTML parser would otherwise discover them. For example, the preload scanner would allow the browser to start downloading a resource specified in an `<img>` element, even when the HTML parser is blocked while fetching and processing resources such as CSS and JavaScript.

To take advantage of the preload scanner, critical resources should be included in HTML markup sent by the server. The following resource loading patterns are not discoverable by the preload scanner:

*   Images loaded by CSS using the `background-image` property. These image references are in CSS, and can't be discovered by the preload scanner.
*   Dynamically-loaded scripts in the form of `<script>` element markup injected into the DOM using JavaScript or modules loaded using [dynamic `import()`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators/import).
*   HTML rendered on the client using JavaScript. Such markup is contained within strings in JavaScript resources, and isn't discoverable by the preload scanner.
*   CSS `@import` declarations.

These resource loading patterns are all late-discovered resources, and therefore don't benefit from the preload scanner. Avoid them whenever possible. If avoiding such patterns _isn't_ possible, however, you may be able to use a `preload` hint to avoid resource discovery delays.

## CSS

CSS determines the presentation and layout of a page. As described earlier, CSS is a render-blocking resource, so optimizing your CSS could have a considerable impact on overall page load time.

### Minification

[Minifying CSS](https://web.dev/articles/minify-css) files reduces the file size of a CSS resource, making them quicker to download. This is accomplished primarily by removing content from a source CSS file such as spaces and other invisible characters, and outputting the result to a newly optimized file:

```
/* Unminified CSS: */

/* Heading 1 */
h1 {
  font-size: 2em;
  color: #000000;
}

/* Heading 2 */
h2 {
  font-size: 1.5em;
  color: #000000;
}
```
```
/* Minified CSS: */
h1,h2{color:#000}h1{font-size:2em}h2{font-size:1.5em}
```

In its most basic form, CSS minification is an effective optimization that could improve your website's FCP, and perhaps even LCP in some cases. Tools such as [bundlers](https://bundlers.tooling.report/) can automatically perform this optimization for you in production builds.

### Remove unused CSS

Before rendering any content, the browser needs to download and parse all style sheets. The time required to complete parsing also includes styles that are unused on the current page. If you are using a bundler that combines all CSS resources into a single file, your users are likely downloading more CSS than needed to render the current page.

To discover unused CSS for the current page, use the [Coverage tool](https://developer.chrome.com/docs/devtools/css/reference/#coverage) in Chrome DevTools.

![A screenshot of the coverage tool in Chrome DevTools. A CSS file is selected in its bottom pane, showing a considerable amount of CSS unused by the current page layout.](https://web.dev/static/learn/performance/optimize-resource-loading/image/fig-1.png)

The coverage tool in Chrome DevTools is useful for detecting CSS (and JavaScript) unused by the current page. It can be used to split CSS files into multiple resources to be loaded by different pages, as opposed to shipping a much larger CSS bundle that can delay rendering of the page.

Removing [unused CSS](https://developer.chrome.com/en/docs/lighthouse/performance/unused-css-rules/) has a two-fold effect: in addition to reducing download time, you're optimizing [render tree](https://web.dev/articles/critical-rendering-path/render-tree-construction) construction, as the browser needs to process fewer CSS rules.

### Avoid CSS `@import` declarations

While it may seem convenient, you should avoid `@import` declarations in CSS:

```
/* Don't do this: */
@import url('style.css');
```

Similarly to how the `<link>` element works in HTML, the `@import` declaration in CSS lets you import an external CSS resource from within a style sheet. The major difference between these two approaches is that the HTML `<link>` element is part of the HTML response, and therefore discovered much sooner than a CSS file downloaded by an `@import` declaration.

The reason for this is that in order for an `@import` declaration to be discovered, the CSS file that contains it must _first_ be downloaded. This results in what is known as a _request chain_ which—in the case of CSS—delays how long it takes for a page to initially render. Another drawback is that style sheets loaded using an `@import` declaration can't be discovered by the preload scanner, and therefore become late-discovered render-blocking resources.

```
<!-- Do this instead: -->
<link rel="stylesheet" href="style.css">
```

In most cases, you can replace the `@import` by using a `<link rel="stylesheet">` element. `<link>` elements allow style sheets to be downloaded _concurrently_ and reduces overall load time, as opposed to `@import` declarations, which downloads style sheets _consecutively_.

### Inline critical CSS

The time it takes to download CSS files can increase a page's FCP. Inlining critical styles in the document `<head>` eliminates the network request for a CSS resource, and—when done correctly—can improve initial load times when a user's browser cache is not primed. The remaining CSS can be loaded [asynchronously](https://www.filamentgroup.com/lab/load-css-simpler/), or appended at the end of the `<body>` element.

```
<head>
  <title>Page Title</title>
  <!-- ... -->
  <style>h1,h2{color:#000}h1{font-size:2em}h2{font-size:1.5em}</style>
</head>
<body>
  <!-- Other page markup... -->
  <link rel="stylesheet" href="non-critical.css">
</body>
```

On the downside, inlining a large amount of CSS adds more bytes to the initial HTML response. Because HTML resources often can't be cached for very long—or at all—this means that the inlined CSS is not cached for subsequent pages that may use the same CSS in external style sheets. Test and measure your page's performance to make sure the trade-offs are worth the effort.

### CSS demos

## JavaScript

JavaScript drives most of the interactivity on the web, but it comes at a cost. Shipping too much JavaScript can make your web page slow to respond during page load, and may even cause responsiveness issues that slow down interactions—both of which can be frustrating for users.

### Render-blocking JavaScript

When loading `<script>` elements without the `defer` or `async` attributes, the browser blocks parsing and rendering until the script is downloaded, parsed, and executed. Similarly, inline scripts block the parser until the script is parsed and executed.

### `async` versus `defer`

`async` and `defer` allow external scripts to load without blocking the HTML parser while scripts (including inline scripts) with `type="module"` are deferred automatically. However, `async` and `defer` have some differences that are important to understand.

![A depiction of various script loading mechanisms, all detailing the parser, fetch, and execution roles based on various attributes used such as async, defer, type='module' and a combination of all three.](https://web.dev/static/learn/performance/optimize-resource-loading/image/fig-2.svg)

Sourced from [https://html.spec.whatwg.org/multipage/scripting.html](https://html.spec.whatwg.org/multipage/scripting.html)

Scripts loaded with `async` are parsed and executed immediately once downloaded, while scripts loaded with `defer` are executed when HTML document parsing is finished—this occurs at the same time as the browser's `DOMContentLoaded` event. Additionally, `async` scripts may execute out-of-order, while `defer` scripts are executed in the order in which they appear in the markup.

### Client-side rendering

Generally, you should avoid using JavaScript to render any critical content or a page's [LCP element](https://web.dev/articles/lcp#what-elements-are-considered). This is known as client-side rendering, and is a technique used extensively in Single Page Applications (SPAs).

Markup rendered by JavaScript sidesteps the preload scanner, as the resources contained within the client-rendered markup [are not discoverable](https://web.dev/articles/preload-scanner#rendering_markup_with_client-side_javascript) by it. This could delay the download of crucial resources, such as an LCP image. The browser only begins downloading the LCP image after the script has executed, and added the element to the DOM. In turn, the script can only be executed after it has been discovered, downloaded, and parsed. This is known as a [critical request chain](https://developer.chrome.com/en/docs/lighthouse/performance/critical-request-chains/) and should be avoided.

Additionally, rendering markup using JavaScript is more likely to generate [long tasks](https://web.dev/articles/long-tasks-devtools) than markup downloaded from the server in response to a navigation request. Extensive use of [client-side rendering of HTML can negatively affect interaction latency](https://web.dev/articles/client-side-rendering-of-html-and-interactivity). This is especially true in cases where [a page's DOM is very large](https://web.dev/articles/dom-size-and-interactivity), which triggers significant rendering work when JavaScript modifies the DOM.

### Minification

Similar to CSS, [minifying JavaScript](https://developer.chrome.com/en/docs/lighthouse/performance/unminified-javascript/) reduces a script resource's file size. This can lead to quicker downloads, allowing the browser to move onto the process of parsing and compiling JavaScript more quickly.

Additionally, minification of JavaScript goes one step further than minifying other assets, such as CSS. When JavaScript is minified, it isn't only stripped of things such as spaces, tabs, and comments, but symbols in the source JavaScript are shortened. This process is sometimes known as _uglification_. To see the difference, take the following JavaScript source code:

```
// Unuglified JavaScript source code:
export function injectScript () {
  const scriptElement = document.createElement('script');
  scriptElement.src = '/js/scripts.js';
  scriptElement.type = 'module';

  document.body.appendChild(scriptElement);
}
```

When the preceding JavaScript source code is uglified, the result may look something like the following code snippet:

```
// Uglified JavaScript production code:
export function injectScript(){const t=document.createElement("script");t.src="/js/scripts.js",t.type="module",document.body.appendChild(t)}
```

In the preceding snippet, you can see that the human readable variable `scriptElement` in the source is shortened to `t`. When applied across a large collection of scripts, the savings can be quite significant, without affecting the features a web site's production JavaScript provides.

If you're using a bundler to process your web site's source code, uglification is often done automatically for production builds. Uglifiers—such as [Terser](https://terser.org/), for example—are also highly configurable, which lets you tweak the aggressiveness of the uglification algorithm to achieve maximum savings. However, the defaults for any uglification tool are usually sufficient to strike the right balance between output size and preservation of capabilities.

### JavaScript demos

## Test your knowledge

What is the best way to load multiple CSS files in the browser?

Multiple `<link>` elements.

The CSS `@import` declaration.

What does the browser preload scanner do?

Detects `<link rel="preload">` elements in an HTML resource.

It is a secondary HTML parser that examines raw markup to discover resources before the DOM parser can in order to discover them sooner.

Why does the browser temporarily block parsing of HTML by default when downloading JavaScript resources?

Because evaluating JavaScript is a very CPU-intensive task, and pausing HTML parsing gives more bandwidth to the CPU to finish loading scripts.

Because scripts can modify or otherwise access the DOM.

To prevent a Flash of Unstyled Content (FOUC).

## Up next: Assisting the browser with resource hints

Now that you have a handle on how resources loaded in the `<head>` element can affect initial page load and various metrics, it's time to move on. In the next module, [resource hints](https://web.dev/learn/performance/resource-hints) are explored, and how they can give valuable hints to the browser to begin loading resources and opening connections to cross-origin servers sooner than the browser otherwise would without them.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
