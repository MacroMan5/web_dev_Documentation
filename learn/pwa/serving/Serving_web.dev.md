# Serving  |  web.dev

**Source URL:** [https://web.dev/learn/pwa/serving?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%2Fserving](https://web.dev/learn/pwa/serving?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%2Fserving)  
**Last Updated:** 2025-05-23T00:56:18.138Z  
**Extracted:** 2025-05-31 16:58:10

---

# Glitch

A key aspects of Progressive Web Apps is that they're reliable; they can load assets quickly, keeping users engaged and providing feedback immediately, even under poor network conditions. How is that possible? Thanks to the service worker `fetch` event.

## The fetch event

The [`fetch`](https://developer.mozilla.org/docs/Web/API/FetchEvent) event lets us intercept every network request made by the PWA in the service worker's scope, for both same-origin and cross-origin requests. In addition to navigation and asset requests, fetching from an installed service worker allows page visits after a site's first load to be rendered without network calls.

The `fetch` handler receives all requests from an app, including URLs and HTTP headers, and lets the app developer decide how to process them.

![The service worker sits between the client and the network.](https://web.dev/static/learn/pwa/serving/image/the-service-worker-sits-b-6649fdd7d05cd.png)

Your service worker can forward a request to the network, respond with a previously cached response, or create a new response. The choice is yours. Here's a simple example:

```
self.addEventListener("fetch", event => {
    console.log(`URL requested: ${event.request.url}`);
});
```

## Responding to a request

When a request comes into your service worker, there are two things you can do; you can ignore it, which lets it go to the network, or you can respond to it. Responding to requests from within your service worker is how you're able to choose what, and how it gets returned to your PWA, even when the user is offline.

To respond to an incoming request, call `event.respondWith()` from within a `fetch` event handler, like this:

```
// fetch event handler in your service worker file
self.addEventListener("fetch", event => {
    const response = .... // a response or a Promise of response
    event.respondWith(response);
});
```

You must call `respondWith()` synchronously and you must return a [Response](https://developer.mozilla.org/docs/Web/API/Response) object. But you can't call `respondWith()` after the fetch event handler has finished, like within an async call. If you need to wait for the complete response, you can pass a Promise to `respondWith()` that resolves with a Response.

### Creating responses

Thanks to the [Fetch API](https://developer.mozilla.org/docs/Web/API/Fetch_API), you can create HTTP responses in your JavaScript code, and those responses can be cached using the Cache Storage API and returned as if they were coming from a web server.

To create a response, create a new `Response` object, setting its body and options such as status and headers:

```
const simpleResponse = new Response("Body of the HTTP response");

const options = {
   status: 200,
   headers: {
    'Content-type': 'text/html'
   }
};
const htmlResponse = new Response("<b>HTML</b> content", options)
```

### Responding from the cache

Now that you know how to serve HTTP responses from a service worker, it's time to use the [Caching Storage interface](https://web.dev/learn/pwa/caching) to store assets on the device.

You can use the cache storage API to check if the request received from the PWA is available in the cache, and if it is, respond to `respondWith()` with it. To do that, you first need to search within the cache. The `match()` function, available at the top-level `caches` interface searches all stores in your origin, or on a single open cache object.

The `match()` function receives an HTTP request or a URL as an argument and it returns a promise that resolves with the Response associated with the corresponding key.

```
// Global search on all caches in the current origin
caches.match(urlOrRequest).then(response => {
   console.log(response ? response : "It's not in the cache");
});

// Cache-specific search
caches.open("pwa-assets").then(cache => {
  cache.match(urlOrRequest).then(response => {
    console.log(response ? response : "It's not in the cache");
  });
});
```

## Caching strategies

Serving files only from the browser cache doesn't fit every use case. For example the user or the browser can evict the cache. That's why you should define your own strategies for delivering assets for your PWA. You're not restricted to one caching strategy. You can define different ones for different URL patterns. For example, you can have one strategy for the minimum UI assets, another for API calls, and a third for image and data URLs. To do this, read `event.request.url` in `ServiceWorkerGlobalScope.onfetch` and parse it through regular expressions or a [URL Pattern](https://web.dev/urlpattern). (At the time of writing, URL Pattern is not supported on all platforms).

The most common strategies are:

Cache First

Searches for a cached response first and falls back to the network if one isn't found.

Network First

Requests a response from the network first and if none is returned, checks for response in the cache.

Stale While Revalidate

Serves a response from the cache, while in the background requests the latest version and saves it to the cache for the next time the asset is requested.

Network-Only

Always replies with a response from the network or errors out. The cache is never consulted.

Cache-Only

Always replies with a response from the cache or errors out. The network will never be consulted. The assets that will be served using this strategy must be added to the cache before they are requested.

### Cache first

Using this strategy, the service worker looks for the matching request in the cache and returns the corresponding Response if it's cached. Otherwise it retrieves the response from the network (optionally, updating the cache for future calls). If there is neither a cache response nor a network response, the request will error. Since serving assets without going to the network tends to be faster, this strategy prioritizes performance over freshness.

![The Cache First strategy](https://web.dev/static/learn/pwa/serving/image/the-cache-strategy-9772ea079508c.png)

```
self.addEventListener("fetch", event => {
   event.respondWith(
     caches.match(event.request)
     .then(cachedResponse => {
       // It can update the cache to serve updated content on the next request
         return cachedResponse || fetch(event.request);
     }
   )
  )
});
```

### Network first

This strategy is the mirror of the Cache First strategy; it checks if the request can be fulfilled from the network and, if it can't, tries to retrieve it from the cache. Like cache first. If there is neither a network response nor a cache response, the request will error. Getting the response from the network is usually slower than getting it from the cache, this strategy prioritizes updated content instead of performance.

![The Network First strategy](https://web.dev/static/learn/pwa/serving/image/the-network-strategy-cb98325f89daa.png)

```
self.addEventListener("fetch", event => {
   event.respondWith(
     fetch(event.request)
     .catch(error => {
       return caches.match(event.request) ;
     })
   );
});
```

### Stale while revalidate

The stale while revalidate strategy returns a cached response immediately, then checks the network for an update, replacing the cached response if one is found. This strategy always makes a network request, because even if a cached resource is found, it will try to update what was in the cache with what was received from the network, to use the updated version in the next request. This strategy, therefore, provides a way for you to benefit from the quick serving of the cache first strategy and update the cache in the background.

![The stale while revalidate strategy](https://web.dev/static/learn/pwa/serving/image/the-stale-while-revalidat-4eb9e02cb6f22.png)

```
self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request).then(cachedResponse => {
        const networkFetch = fetch(event.request).then(response => {
          // update the cache with a clone of the network response
          const responseClone = response.clone()
          caches.open(url.searchParams.get('name')).then(cache => {
            cache.put(event.request, responseClone)
          })
          return response
        }).catch(function (reason) {
          console.error('ServiceWorker fetch failed: ', reason)
        })
        // prioritize cached response over network
        return cachedResponse || networkFetch
      }
    )
  )
})
```

### Network only

The network only strategy is similar to how browsers behave without a service worker or the Cache Storage API. Requests will only return a resource if it can be fetched from the network. This is often useful for resources like online-only API requests.

![The Network only strategy](https://web.dev/static/learn/pwa/serving/image/the-network-strategy-acff1b21e751c.png)

### Cache only

The cache only strategy ensures that requests never go to the network; all incoming requests are responded to with a pre-populated cache item. The following code uses the `fetch` event handler with the `match` method of the cache storage to respond cache only:

```
self.addEventListener("fetch", event => {
   event.respondWith(caches.match(event.request));
});
```

![Cache only strategy.](https://web.dev/static/learn/pwa/serving/image/cache-strategy-31f1d2915a6c5.png)

### Custom strategies

While the above are common caching strategies, you are in charge of your service worker and how requests are handled. If none of these work for your needs, create your own.

You can, for example, use a network first strategy with a timeout to prioritize updated content, but only if the response appears within a threshold you set. You can also merge a cached response with a network response and build a complex response from the service worker.

## Updating assets

Keeping your PWA's cached assets up-to-date can be a challenge. While the stale while revalidate strategy is one way to do so, it's not the only one. In the [Update chapter](https://web.dev/learn/pwa/update) you will learn different techniques to keep your app's content and assets updated.

## Resources

*   [Fetch event on MDN](https://developer.mozilla.org/docs/Web/API/FetchEvent)
*   [The Offline Cookbook](https://web.dev/articles/offline-cookbook)
*   [Cache Match on MDN](https://developer.mozilla.org/docs/Web/API/Cache/match)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
