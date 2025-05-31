# Caching  |  web.dev

**Source URL:** [https://web.dev/learn/pwa/caching?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%2Fcaching](https://web.dev/learn/pwa/caching?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%2Fcaching)  
**Last Updated:** 2025-05-23T00:56:12.560Z  
**Extracted:** 2025-05-31 16:58:10

---

# Glitch

Cache storage is a powerful tool. It makes your apps less dependent on network conditions. With good use of caches you can make your web app available offline and serve your assets as fast as possible in any network condition. As mentioned in [Assets and Data](https://web.dev/learn/pwa/assets-and-data) you can decide the best strategy for caching the necessary assets. To manage the cache your service worker interacts with the [Cache Storage API](https://developer.mozilla.org/docs/Web/API/CacheStorage).

The Cache Storage API is available from different contexts:

*   The window context (your PWA's main thread).
*   The service worker.
*   Any other workers you use.

One advantage of managing your cache using service workers is that its lifecycle is not tied to the window, which means you are not blocking the main thread. Be aware that to use the Cache Storage API most of these contexts have to be under a TLS connection.

## What to cache

The first question you may have about caching is what to cache. While there is no single answer to that question, you can start with all the minimum resources that you need to render the user interface.

Those resources should include:

*   The main page HTML (your app's start\_url).
*   CSS stylesheets needed for the main user interface.
*   Images used in the user interface.
*   JavaScript files required to render the user interface.
*   Data, such as a JSON file, required to render a basic experience.
*   Web fonts.
*   On a multi-page application, other HTML documents that you want to serve fast or while offline.

### Offline-ready

While being offline-capable is one of the requirements for a Progressive Web App, it's essential to understand that not every PWA needs a full offline experience, for example cloud gaming solutions or crypto assets apps. Therefore, it's OK to offer a basic user interface guiding your users through those situations.

Your PWA should not render a browser's error message saying that the web rendering engine couldn't load the page. Instead use your service worker to show your own messaging, avoiding a generic and confusing browser error.

There are many different caching strategies you could use depending on the needs of your PWA. That's why it is important to design your cache usage to provide a fast and reliable experience. For example if all your app assets will download fast, don't consume a lot of space, and don't need to be updated in every request, caching all your assets would be a valid strategy. If on the other hand you have resources that need to be the latest version you might want to consider not caching those assets at all.

## Using the API

Use the Cache Storage API to define a set of caches within your origin, each identified with a string name you can define. Access the API through the `caches` object, and the `open` method enables the creation, or opening of an already created cache. The open method returns a promise for the cache object.

```
caches.open("pwa-assets")
.then(cache => {
  // you can download and store, delete or update resources with cache arguments
});
```

### Downloading and storing assets

To ask the browser to download and store the assets use the `add` or `addAll` methods. The `add` method makes a request and stores one HTTP response, and `addAll` a group of HTTP responses as a transaction based on an array of requests or URLs.

```
caches.open("pwa-assets")
.then(cache => {
  cache.add("styles.css"); // it stores only one resource
  cache.addAll(["styles.css", "app.js"]); // it stores two resources
});
```

The cache storage interface stores the entirety of a response including all the headers and the body. Consequently, you can retrieve it later using an HTTP request or a URL as a key. You will see how to do that in [the Serving chapter](https://web.dev/learn/pwa/serving).

### When to cache

In your PWA, you are in charge of deciding when to cache files. While one approach is to store as many assets as possible when the service worker is installed, it is usually not the best idea. Caching unnecessary resources wastes bandwidth and storage space and could cause your app to serve unintended outdated resources.

You don't need to cache all the assets at once, you can cache assets many times during the lifecycle of your PWA, such as:

*   On installation of the service worker.
*   After the first page load.
*   When the user navigates to a section or route.
*   When the network is idle.

You can request caching new files in the main thread or within the service worker context.

### Caching assets in a service worker

One of the most common scenarios is to cache a minimum set of assets when the service worker is installed. To do that, you can use the cache storage interface within the `install` event in the service worker.

Because the service worker thread can be stopped at any time, you can request the browser to wait for the `addAll` promise to finish to increase the opportunity of storing all the assets and keeping the app consistent. The following example demonstrates how to do this, using the `waitUntil` method of the event argument received in the service worker event listener.

```
const urlsToCache = ["/", "app.js", "styles.css", "logo.svg"];
self.addEventListener("install", event => {
   event.waitUntil(
      caches.open("pwa-assets")
      .then(cache => {
         return cache.addAll(urlsToCache);
      });
   );
});
```

The [`waitUntil()` method](https://developer.mozilla.org/docs/Web/API/ExtendableEvent/waitUntil) receives a promise and asks the browser to wait for the task in the promise to resolve (fulfilled or failed) before terminating the service worker process. You may need to chain promises and return the `add()` or `addAll()` calls so that a single result gets to the `waitUntil()` method.

You can also handle promises using the async/await syntax. In that case, you need to create an asynchronous function that can call `await` and that returns a promise to `waitUntil()` after it's called, as in the following example:

```
const urlsToCache = ["/", "app.js", "styles.css", "logo.svg"];
self.addEventListener("install", (event) => {
   let cacheUrls = async () => {
      const cache = await caches.open("pwa-assets");
      return cache.addAll(urlsToCache);
   };
   event.waitUntil(cacheUrls());
});
```

### Cross-domain requests and opaque responses

Your PWA can download and cache assets from your origin and cross-domains, such as content from third-party CDNs. With a cross-domain app, the cache interaction is very similar to same-origin requests. The request is executed and a copy of the response is stored in your cache. As with other cached assets it is only available to be used in your app's origin.

The asset will be stored as an [opaque response](https://fetch.spec.whatwg.org/#concept-filtered-response-opaque), which means your code won't be able to see or modify the contents or headers of that response. Also, opaque responses don't expose their actual size in the storage API, affecting quotas. Some browsers expose large sizes, such as 7Mb no matter if the file is just 1Kb.

### Updating and deleting assets

You can update assets using `cache.put(request, response)` and delete assets with `delete(request)`.

Check the [Cache object documentation](https://developer.mozilla.org/docs/Web/API/Cache) for more details.

## Debugging Cache Storage

Many browsers offer a way to debug the contents of cache storage within their DevTools Application tab. There, you can see the contents of every cache within the current origin. We'll cover more about these tools in the [Tools and Debug chapter](https://web.dev/learn/pwa/tools-and-debug).

![Chrome DevTools debugging Cache Storage contents.](https://web.dev/static/learn/pwa/caching/image/chrome-devtools-debugging-865b4a170f79c.png)

## Resources

*   [Cache Storage on MDN](https://developer.mozilla.org/docs/Web/API/CacheStorage)
*   [The Cache API: A quick guide](https://web.dev/articles/cache-api-quick-guide)
*   [The Offline Cookbook](https://web.dev/articles/offline-cookbook)
*   [Caching Demystified: Inspect, Clear, and Disable Caches](https://developer.chrome.com/blog/devtools-tips-36)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
