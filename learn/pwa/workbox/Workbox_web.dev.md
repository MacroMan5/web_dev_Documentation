# Workbox  |  web.dev

**Source URL:** [https://web.dev/learn/pwa/workbox?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%2Fworkbox](https://web.dev/learn/pwa/workbox?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%2Fworkbox)  
**Last Updated:** 2025-05-23T00:56:34.237Z  
**Extracted:** 2025-05-31 16:58:10

---

# Workbox  |  web.dev

Maintaining your service worker and cache storage logic can be a challenge as your PWA grows. [Workbox](https://developer.chrome.com/docs/workbox/what-is-workbox), is a set of open-source libraries to help with that. Workbox encapsulates the low-level APIs, like the Service Worker API and Cache Storage API, and exposes more developer-friendly interfaces.

Some tasks that it can help with are matching caching strategies to paths (or routing patterns), working with streams, and using features like background sync with proper fallbacks.

Workbox can help you with managing your asset caching and serving needs. It's also the most used library for service workers; used by [54% of mobile sites](https://almanac.httparchive.org/en/2022/pwa#workbox-usage) and it is used in many build tools and CLIs, including the Angular CLI, Create-React-App, and Vue CLI. There are plugins to most other libraries and frameworks, too, such as Next.js.

54%

Mobile sites with service workers use the Workbox library

## Workbox modules

Workbox includes several [libraries](https://developer.chrome.com/docs/workbox/modules)—called modules internally—each focused on a different aspect of managing your assets and service worker behavior.

Workbox modules work in different contexts, such as:

*   **Within a service worker context**: you import the modules you need and use them from your service worker file, for example to help manage caching and serve files with different strategies.
*   **Within the main `window` context**: helping to register a service worker and communicating with it
*   **As part of a build system**: for example, webpack, for purposes such as creating a manifest of your assets, or even generating your entire service worker.

Some popular modules are:

*   [workbox-routing](https://developer.chrome.com/docs/workbox/modules/workbox-routing): When the service worker intercepts requests this module routes those requests to different functions that provide responses; it's an implementation of the `fetch` event handler as mentioned in the [Serving chapter](https://web.dev/learn/pwa/serving).
*   [workbox-strategies](https://developer.chrome.com/docs/workbox/modules/workbox-strategies): A set of runtime caching strategies that handle responding to a request, such as cache first and stale while revalidate; it's an implementation of the different strategies mentioned in the [Serving chapter](https://web.dev/learn/pwa/serving).
*   [workbox-precaching](https://developer.chrome.com/docs/workbox/modules/workbox-precaching): It's an implementation of caching files in the `install` event handler of the service worker (also known as precaching), as mentioned in the [Caching chapter](https://web.dev/learn/pwa/caching). With this module you can easily precache a set of files and efficiently manage updates to those assets. We'll cover updating assets in the [Update chapter](https://web.dev/learn/pwa/update).
*   [workbox-expiration](https://developer.chrome.com/docs/workbox/modules/workbox-expiration): It is a plugin used with the caching strategies to remove cached requests based on the number of items in a cache or based on the age of the cached request. It helps manage your caches and sets limits on time and the number of items in each cache.
*   [workbox-window](https://developer.chrome.com/docs/workbox/modules/workbox-window): A set of modules intended to run in the window context, which is to say, inside of your PWA web pages. You can simplify the process of service worker registration and updates and enable easier communication between code running in the service worker context and the window context.

## Using Workbox

Workbox provides different ways to integrate into your PWA. You can choose which fits best with your app's architecture:

*   [Workbox CLI](https://developer.chrome.com/docs/workbox/modules/workbox-cli): A command-line utility that generates a complete service worker, injects a precache manifest, or copies needed Workbox files.
*   [Workbox Build](https://developer.chrome.com/docs/workbox/modules/workbox-build): An npm module that generates a complete service worker, injects a precache manifest, and copies the Workbox files. This is meant to be integrated with your own build process.
*   [workbox-sw](https://developer.chrome.com/docs/workbox/modules/workbox-sw): A way to load Workbox service worker packages from a CDN that doesn't use a build process.

Workbox CLI provides a wizard that steps you through creating your service worker. To run the wizard, type the following at a command line:

```
npx workbox-cli wizard
```

![Workbox CLI in action in a terminal](https://web.dev/static/learn/pwa/workbox/image/workbox-cli-action-a-te-cdda129657c2f.png)

## Caching and serving with Workbox

A common use of Workbox is using the routing and strategies modules together to cache and serve files.

The module [_workbox-strategies_](https://developer.chrome.com/docs/workbox/modules/workbox-strategies) provides, out of the box, the caching strategies discussed in the [Assets and data](https://web.dev/learn/pwa/assets-and-data) and [Serving](https://web.dev/learn/pwa/serving) chapters.

The [_workbox-routing_](https://developer.chrome.com/docs/workbox/modules/workbox-routing) module helps to sort incoming requests to your service worker and match them to the caching strategies or functions to get responses for those requests.

After the matching of routes to strategies, Workbox also offers the ability to filter which responses will be added to the cache with the [_workbox-cacheable-response_ plugin](https://developer.chrome.com/docs/workbox/modules/workbox-cacheable-response). With this plugin you can for example cache only responses that returned without errors.

The following code sample uses a cache first strategy (via the `CacheFirst` module) to cache and serve page navigations.

```
import { registerRoute } from 'workbox-routing';
import { CacheFirst } from 'workbox-strategies';
import { CacheableResponsePlugin } from 'workbox-cacheable-response';

const pageStrategy = new CacheFirst({
  // Put all cached files in a cache named 'pages'
  cacheName: 'pages',
  plugins: [
    // Only requests that return with a 200 status are cached
    new CacheableResponsePlugin({
      statuses: [200],
    }),
  ],
});
```

The plugin allows you to tap into Workbox's caching and request resolution lifecycle. Here, the `CacheableResponsePlugin` is used to only cache requests that result in a 200 status, preventing bad requests from being saved into the cache.

With the strategy created, it's time to register a route to use it. The following example calls `registerRoute()`, passing a Request object to its callback. If `request.mode` is `"navigate"` it uses the `CacheFirst` strategy (here called `pageStrategy`) defined in the previous code example.

```
// Cache page navigations (HTML) with a Cache First strategy
registerRoute( ({ request }) => request.mode === 'navigate',
  pageStrategy );
```

Read the [Workbox documentation](https://developer.chrome.com/docs/workbox) for more examples and best practices.

## Offline fallback

The _workbox-routing_ module also has an exported `setCatchHandler()`, that provides handling if a route throws an error. You can use this to set up an offline fallback to notify users that their requested route isn't currently available.

Here, a combination of Workbox and the Cache Storage API provides an offline fallback using a cache-only strategy. First, during the service worker's install lifecycle, the `offline-fallbacks` cache is opened, and the array of offline fallbacks is added to the cache.

```
import { setCatchHandler } from 'workbox-routing';

// Warm the cache when the service worker installs
self.addEventListener('install', event => {
  const files = ['/offline.html']; // you can add more resources here
  event.waitUntil(
    self.caches.open('offline-fallbacks')
        .then(cache => cache.addAll(files))
  );
});
```

Then, in `setCatchHandler()`, the destination of the request that threw an error is determined, and the `offline-fallbacks` cache is opened. If the destination is a document, the content of the offline fallback is returned to the user. If that doesn't exist, or the destination isn't a document (such as an image or stylesheet), an error response is returned. You can extend this pattern not just for documents but for images, videos, fonts, really anything that you'd want to provide as an offline fallback.

```
// Respond with the fallback if a route throws an error
setCatchHandler(async (options) => {
  const destination = options.request.destination;
  const cache = await self.caches.open('offline-fallbacks');
  if (destination === 'document') {
    return (await cache.match('/offline.html')) || Response.error();
  }
  return Response.error();
});
```

## Recipes

Several routing and caching patterns, like `NetworkFirst` navigations and offline fallbacks, are common enough to be encapsulated into reusable recipes. Check [workbox-recipes](https://developer.chrome.com/docs/workbox/modules/workbox-recipes) as they can help you if they provide a solution suitable for your architecture. They are usually available as one line of code that you need to add to your service worker's code.

### Caching and updating assets

Caching assets also involves updating them. Workbox helps with updating your assets in whatever way you decide is best. It could be keeping them updated if they change on the server, or waiting until you have a new version of your app. You'll learn more about updating in the [Update chapter](https://web.dev/learn/pwa/update).

## Play with Workbox

You can play with Workbox right away using the following code lab:

## Resources

*   [Get Started with Workbox](https://developer.chrome.com/docs/workbox)
*   [Workbox Modules](https://developer.chrome.com/docs/workbox/modules)
*   [The ways of Workbox](https://developer.chrome.com/docs/workbox/the-ways-of-workbox)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
