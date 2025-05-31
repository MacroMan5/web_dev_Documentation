# General HTML performance considerations  |  web.dev

**Source URL:** [https://web.dev/learn/performance/general-html-performance?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%2Fgeneral-html-performance](https://web.dev/learn/performance/general-html-performance?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%2Fgeneral-html-performance)  
**Last Updated:** 2025-05-23T01:13:41.058Z  
**Extracted:** 2025-05-31 16:58:10

---

# Glitch

The first step in building a website that loads quickly is to receive a timely response from the server for a page's HTML. When you enter a URL in the browser's address bar, the browser sends a [`GET` request](https://developer.mozilla.org/docs/Web/HTTP/Methods/GET) to the server to retrieve it. The first request for a web page is for an HTML resource—and ensuring that HTML arrives quickly with minimal delays is a key performance goal.

That initial request for HTML goes through several steps, each of which take some time. Reducing the time spent on each step gives you a faster [Time to First Byte (TTFB)](https://web.dev/articles/ttfb). While TTFB is not the sole metric you should focus on when it comes to how fast pages load, a high TTFB _does_ make it challenging to reach the designated "good" thresholds for metrics such as [Largest Contentful Paint (LCP)](https://web.dev/articles/lcp) and [First Contentful Paint (FCP)](https://web.dev/articles/fcp).

## Minimize redirects

When a resource is requested, the server may respond with a redirect, either with a permanent redirect (a `301 Moved Permanently` response) or a temporary one (a `302 Found` response).

Redirects slow down page load speed because it requires the browser to make an additional HTTP request at the new location to retrieve the resource. There are two types of redirects:

1.  _Same-origin redirects_ that occur entirely within your origin. These types of redirects are completely within your control, as the logic for managing them resides entirely on your web server.
2.  _Cross-origin redirects_ that are initiated by another origin. These types of redirects are typically out of your control.

Cross-origin redirects are often used by ads, URL-shortening services, and other third party services. Though cross-origin redirects are outside of your control, you may still want to check that you avoid multiple redirects—for example, having an ad that links to an HTTP page which in turn redirects to its HTTPS equivalent, or a cross-origin redirect that arrives to your origin, but then triggers a same-origin redirect.

## Cache HTML responses

Caching HTML responses is difficult, since the response may include links to other critical resources such as CSS, JavaScript, images, and other resource types. These resources may include [a unique fingerprint](https://bundlers.tooling.report/hashing/) in their respective filenames, which changes based on a file's contents. This means that your cached HTML document may become stale following a deployment, as it would contain references to outdated subresources.

Nonetheless, a short cache lifetime—rather than no caching—can have benefits such as allowing a resource to be cached at a CDN—reducing the number of requests that are served from the origin server—and in the browser, allowing resources to be revalidated rather than downloaded again. This approach works best for static content that doesn't change in any context, and an appropriate time to cache the resources can be set to some number of minutes you deem appropriate. Five minutes for static HTML resources is a safe bet, and ensures that periodic updates don't go unnoticed.

If a page's HTML contents are personalized in some way—such as for an authenticated user—you very likely don't want to cache content at all for a variety of concerns, including security and freshness. If an HTML response is cached by the user's browser, you are unable to invalidate the cache. It's therefore best to avoid caching HTML altogether in such cases.

A cautious approach to caching HTML could be to use the [`ETag`](https://developer.mozilla.org/docs/Web/HTTP/Headers/ETag) or [`Last-Modified`](https://developer.mozilla.org/docs/Web/HTTP/Headers/Last-Modified) response headers. An `ETag`—otherwise known as an entity tag—header is an identifier that uniquely represents the requested resource, often by using a [hash of the resource's contents](https://en.wikipedia.org/wiki/Hash_function):

```
ETag: "33a64df551425fcc55e4d42a148795d9f25f89d4"
```

Whenever the resource changes, a new `ETag` value must be generated. On subsequent requests, the browser sends the `ETag` value through the [`If-None-Match` request header](https://developer.mozilla.org/docs/Web/HTTP/Headers/If-None-Match). If the `ETag` on the server matches the one sent by the browser, the server responds with a `304 Not Modified` response, and the browser uses the resource from the cache. While this still incurs network latency, a `304 Not Modified` response is _much_ smaller than an entire HTML resource.

However, the network latency involved in revalidating a resource's freshness is still its own sort of downside. As with many other aspects of web development, trade-offs and compromises are inevitable. It's up to you to figure out if the additional effort to cache HTML in this way is worth it, or if it's best to stay on the safe side and not bother caching HTML content at all.

## Measure server response times

If a response is not cached, the server's response time is highly dependent on your hosting provider and backend application stack. A web page that serves a dynamically generated response—such as fetching data from a database, for example—may well have a higher TTFB than a static web page that can be served immediately without significant compute time on the backend. Displaying a loading spinner and then fetching all data on the client side moves the effort from a more predictable server-side environment to a potentially unpredictable client-side one. Minimizing client-side effort usually results in improved user-centric metrics.

If users are experiencing a slow TTFB in [the field](https://web.dev/articles/lab-and-field-data-differences#field_data), you can expose information on where time was spent on the server through the use of the [`Server-Timing` response header](https://developer.mozilla.org/docs/Web/HTTP/Headers/Server-Timing):

```
Server-Timing: auth;dur=55.5, db;dur=220
```

A `Server-Timing` header's value can include multiple metrics, as well as a duration for each one. This data can then be collected from users [in the field using the Navigation Timing API](https://web.dev/articles/navigation-and-resource-timing) and analyzed to see if users are experiencing delays. In the preceding code snippet, the response header includes two timings:

*   The time to authenticate a user (`auth`), which took 55.5 milliseconds.
*   The database access time (`db`), which took 220 milliseconds.

You may also want to review your hosting infrastructure and confirm that you have adequate resources to handle the traffic your website is receiving. Shared hosting providers are often susceptible to a high TTFB, and dedicated solutions that provide faster response times may be more costly.

## Compression

Text-based responses such as HTML, JavaScript, CSS, and SVG images should be compressed to reduce their transfer size over the network in order for them to download more quickly. The most widely used compression algorithms are gzip and Brotli. Brotli results in about a 15% to 20% improvement over gzip.

Compression is often automatically set up by most web hosting providers, but there are some important things to consider if you're in a position to configure or tweak compression settings yourself:

1.  **Use Brotli where possible.** As stated previously, Brotli provides a fairly noticeable improvement over gzip, and [Brotli is supported in all major browsers](https://caniuse.com/brotli). Use Brotli when possible, but if your website is used by a high number of users on legacy browsers, be sure that gzip is used as a fallback, as any compression is better than no compression at all.
2.  **File size matters.** Very small resources—less than 1 KiB—don't compress very well, or sometimes don't even compress at all. Effectiveness of any type of data compression depends on having a large amount of data that a compression algorithm can work with in order to find more compressible bits of data. The larger a file is, the better compression works—however, don't ship very large resources for the mere fact that they can be compressed more effectively. Large resources—such as JavaScript and CSS for example—take significantly more time to parse and evaluate after the browser has _decompressed_ them, and may change more frequently even if they've only changed marginally, as any changes result in a different [file hash](https://bundlers.tooling.report/hashing/).
3.  **Understand dynamic versus static compression.** Dynamic and static compression are differing approaches to _when_ a resource should be compressed. Dynamic compression compresses a resource _at the time it's requested_, and sometimes _every time_ it is requested. On the other hand, static compression compresses files _ahead_ of time, requiring no compression to be performed at the time of the request. Static compression removes the latency involved in compression itself, which can add to server response times in the case of dynamic compression. Static resources—such as JavaScript, CSS, and SVG images—should be statically compressed, whereas HTML resources—_especially_ if they are dynamically generated for authenticated users—should be dynamically compressed.

Getting compression right on your own is challenging, and it's often best to let a Content Delivery Network (CDN)—which is discussed in the next section—to handle this for you. However, knowing these concepts can help you to discern whether your hosting provider is using compression properly. That knowledge can help you to find opportunities to improve your compression settings so that they yield the maximum benefit for your website.

## Content Delivery Networks (CDNs)

A [Content Delivery Network (CDN)](https://web.dev/articles/content-delivery-networks) is a distributed network of servers that cache resources from your origin server, and in turn, serves them from edge servers that are physically closer to your users. The physical proximity to your users reduces [round-trip time (RTT)](https://en.wikipedia.org/wiki/Round-trip_delay), while optimizations such as HTTP/2 or HTTP/3, caching, and compression allow the CDN to serve content more quickly than if it would be fetched from your origin server. Utilizing a CDN can significantly improve your website's TTFB in some cases.

## Test your knowledge

What type of redirect is completely within your control?

The `Server-Timing` header can contain multiple metrics.

Which type of server is most likely to be physically closest to your end users?

Your website's origin server.

A Content Delivery Network's (CDN) edge servers.

## Up next: Understanding the critical path

Now that you're familiar with some of the performance considerations involved with your website's HTML, you're in a better position to ensure that it can load as quickly as possible—but that's only the beginning of learning web performance. Next up, the theory behind the [the critical rendering path](https://web.dev/learn/performance/understanding-the-critical-path) is covered. This module describes key concepts such as render-blocking and parsing-blocking resources, and the role they play in getting a page's initial rendering in the browser as quickly as possible.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
