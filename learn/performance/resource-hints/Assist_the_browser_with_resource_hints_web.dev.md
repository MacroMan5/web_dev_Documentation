# Assist the browser with resource hints  |  web.dev

**Source URL:** [https://web.dev/learn/performance/resource-hints?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%2Fresource-hints](https://web.dev/learn/performance/resource-hints?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%2Fresource-hints)  
**Last Updated:** 2025-05-23T01:14:01.366Z  
**Extracted:** 2025-05-31 16:58:10

---

# Glitch

In the last module about [optimizing resource loading](https://web.dev/learn/performance/optimize-resource-loading), you learned how various page resources such as CSS and JavaScript can affect page load speed, and how you can optimize them and their delivery to speed up the rendering of a page. This is the perfect time to move into a more advanced aspect of resource loading, and that involves helping the browser to load them faster by using resource hints.

Resource hints can help developers further optimize page load time by informing the browser how to load and prioritize resources. An initial set of resource hints such as `preconnect` and `dns-prefetch` were the first to be introduced. Over time, however, `preload`, and the Fetch Priority API have followed to provide additional capabilities.

Resource hints instruct the browser to perform certain actions ahead of time that could improve loading performance. Resource hints can perform actions such as performing early DNS lookups, connecting to servers ahead of time, and even fetching resources before the browser would ordinarily discover them.

Resource hints may be specified in HTML—most often early on in the `<head>` element—or [set as an HTTP header](https://almanac.httparchive.org/en/2021/resource-hints#http-header). For the scope of this module, [`preconnect`](https://www.w3.org/TR/resource-hints/#dfn-preconnect), [`dns-prefetch`](https://developer.mozilla.org/docs/Web/Performance/dns-prefetch), and [`preload`](https://developer.mozilla.org/docs/Web/HTML/Link_types/preload) are covered, as well as the speculative fetching behaviors that [`prefetch`](https://developer.mozilla.org/docs/Web/HTML/Attributes/rel/prefetch) provides.

## `preconnect`

The `preconnect` hint is used to establish a connection to another origin from where you are fetching critical resources. For example, you may be hosting your images or assets on a CDN or other cross-origin:

```
<link rel="preconnect" href="https://example.com">
```

By using `preconnect`, you anticipate that the browser plans to connect to a specific cross-origin server in the _very near future_, and that the browser should open that connection as soon as possible, ideally before waiting for the HTML parser or preload scanner to do so.

If you have a large amount of cross-origin resources on a page, use `preconnect` for those resources which are the most critical to the current page.

![A screenshot of connection timings for a resource in the network panel of Chrome DevTools. The connection setup includes stall time, proxy negotiation, DNS lookup, connection setup, and TLS negotiation.](https://web.dev/static/learn/performance/resource-hints/image/fig-1.png)

A visualization of connection timings as seen in the network panel of Chrome DevTools. The timings within the red box are those involved in setting up a connection with a cross-origin server, which `preconnect` can alleviate by establishing connections sooner, rather than at the time of discovery of the cross-origin resource.

A [common use case for `preconnect` is Google Fonts](https://almanac.httparchive.org/en/2021/resource-hints#fig-14). Google Fonts recommends that you `preconnect` to the `https://fonts.googleapis.com` domain that serves the `@font-face` declarations and to the `https://fonts.gstatic.com` domain that serves the font files.

```
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```

The `crossorigin` attribute is used to indicate whether a resource must be fetched using [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/docs/Web/HTTP/CORS). When using the `preconnect` hint, if the resource being downloaded from the origin uses CORS—such as font files—then you need to add the `crossorigin` attribute to the `preconnect` hint.

## `dns-prefetch`

While opening connections to cross-origin servers early can significantly improve initial page load time, it may not be either reasonable or possible to establish connections to many cross-origin servers at once. If you're concerned that you may be overusing `preconnect`, a much less costly resource hint is the `dns-prefetch` hint.

Per its name, `dns-prefetch` doesn't establish a _connection_ to a cross-origin server, but rather just performs the [DNS lookup](https://en.wikipedia.org/wiki/Domain_Name_System#Address_resolution_mechanism) for it ahead of time. A _DNS lookup_ occurs when a domain name is resolved to its underlying IP address. While layers of DNS caches at the device and network levels help to make this a generally fast process, it still takes some amount of time.

```
<link rel="dns-prefetch" href="https://fonts.googleapis.com">
<link rel="dns-prefetch" href="https://fonts.gstatic.com">
```

DNS lookups are fairly inexpensive, and because of their relatively small cost, they may be a more appropriate tool in some cases than a `preconnect`. In particular, it may be a desirable resource hint to use in cases of links that navigate to other websites that you think the user is likely to follow. [dnstradamus](https://github.com/malchata/dnstradamus) is one such tool that does this automatically using JavaScript, and uses the [Intersection Observer API](https://developer.mozilla.org/docs/Web/API/Intersection_Observer_API) to inject `dns-prefetch` hints into the current page's HTML when links to other websites are scrolled into the user's viewport.

## `preload`

The `preload` directive is used to initiate an early request for a resource required for rendering the page:

```
<link rel="preload" href="/lcp-image.jpg" as="image">
```

`preload` directives should be limited to late-discovered critical resources. The most common use cases are font files, CSS files fetched through `@import` declarations, or CSS `background-image` resources that are likely to be [Largest Contentful Paint (LCP) candidates](https://web.dev/articles/lcp#what-elements-are-considered). In such cases, these files wouldn't be discovered by the preload scanner as the resource is referenced in external resources.

Similarly to `preconnect`, the `preload` directive requires the `crossorigin` attribute if you are preloading a CORS resource—such as fonts. If you don't add the `crossorigin` attribute—or add it for non-CORS requests—then the resource is downloaded by the browser _twice_, wasting bandwidth that could have been better spent on other resources.

```
<link rel="preload" href="/font.woff2" as="font" crossorigin>
```

In the preceding HTML snippet, the browser is instructed to preload `/font.woff2` using a CORS request—even if `/font.woff2` is on the same domain.

## `prefetch`

The `prefetch` directive is used to initiate a low priority request for a resource likely to be used for future navigations:

```
<link rel="prefetch" href="/next-page.css" as="style">
```

This directive largely follows the same format as the `preload` directive, only the `<link>` element's `rel` attribute uses a value of `"prefetch"` instead. Unlike the `preload` directive, however, `prefetch` is largely speculative in that you're initiating a fetch for a resource for a future navigation that may or may not happen.

There are times when `prefetch` can be beneficial—for example, if you've identified a user flow on your website that most users follow to completion, a `prefetch` for a render-critical resource for those future pages can help to reduce load times for them.

## Fetch Priority API

You can use the [`Fetch Priority API`](https://web.dev/articles/fetch-priority) through its `fetchpriority` attribute to increase the priority of a resource. You can use the attribute with `<link>`, `<img>`, and `<script>` elements.

```
<div class="gallery">
  <div class="poster">
    <img src="img/poster-1.jpg" fetchpriority="high">
  </div>
  <div class="thumbnails">
    <img src="img/thumbnail-2.jpg" fetchpriority="low">
    <img src="img/thumbnail-3.jpg" fetchpriority="low">
    <img src="img/thumbnail-4.jpg" fetchpriority="low">
  </div>
</div>
```

By default, images are fetched with a lower priority. After layout, if the image is found to be within the initial viewport, the priority is increased to **High** priority. In the preceding HTML snippet, `fetchpriority` immediately tells the browser to download the larger LCP image with a **High** priority, while the less important thumbnail images are downloaded with a lower priority.

Modern browsers load resources in two phases. The first phase is reserved for critical resources and ends once all blocking scripts have been downloaded and executed. During this phase, **Low** priority resources may be delayed from downloading. By using `fetchpriority="high"` you can increase the priority of a resource, enabling the browser to download it during the first phase.

## Resource hints demos

## Test your knowledge

What does the `preconnect` resource hint do?

Opens a connection to a cross-origin server, including the DNS lookup, as well as connection and TLS negotiation ahead of when the browser would otherwise discover it.

Performs only a DNS lookup for the cross-origin server.

What does the Fetch Priority API let you do?

Specify the relative priority for `<link>`, `<img>`, and `<script>` elements.

Specify the priority at which the current page's HTML is downloaded.

When should you use the `prefetch` hint?

When you have _high confidence_ that the resources or pages you intend to prefetch are needed by the user.

If the user has not stated an explicit preference for reduced data usage.

For any and all resources or pages the user could need, whether or not they actually need them in the future.

## Up next: Image performance

By now, you're probably starting to feel pretty confident about your knowledge of general performance considerations when it comes to page HTML, the `<head>` element, and resource hints. However, there are additional optimizations that are specific to different resource types that pages commonly load. Next up, [image performance](https://web.dev/learn/performance/image-performance) is covered in the next module, which can help you to get your website's images loading as fast as they possibly can, regardless of the user's device.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
