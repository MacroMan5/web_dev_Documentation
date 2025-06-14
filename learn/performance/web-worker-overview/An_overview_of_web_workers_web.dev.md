# An overview of web workers  |  web.dev

**Source URL:** [https://web.dev/learn/performance/web-worker-overview?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%2Fweb-worker-overview](https://web.dev/learn/performance/web-worker-overview?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%2Fweb-worker-overview)  
**Last Updated:** 2025-05-23T01:15:12.639Z  
**Extracted:** 2025-05-31 16:58:10

---

# An overview of web workers | web.dev

An overview of web workers

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

Much of the content in this course so far has focused on concepts such as general HTML performance considerations, resource hints, optimization of various resource types to improve initial page load time and responsiveness to user input, as well as lazy loading specific resources.

However, there's one aspect of performance regarding JavaScript that hasn't been covered yet in this course, and that's the role of web workers in improving input responsiveness, which this and the next module covers.

JavaScript is often described as a single-threaded language. In practice, this refers to the _main thread_, which is the single thread where the browser does most of the work that you see in the browser. This work includes tasks involved in things such as scripting, some types of rendering work, HTML and CSS parsing, and other kinds of user-facing work that drives the user experience. In truth, browsers _do_ use other threads to do work that you, the developer, don't typically have direct access to—such as [GPU threads](https://www.chromium.org/developers/design-documents/gpu-accelerated-compositing-in-chrome/).

Where JavaScript is concerned, you're generally confined to doing work on the main thread—but only by default. It _is_ possible to register and use additional threads in JavaScript. The feature that allows for multi-threading in JavaScript is known as [the Web Workers API](https://developer.mozilla.org/docs/Web/API/Web_Workers_API/Using_web_workers).

Web workers are useful when you have computationally expensive work that just can't be run on the main thread without causing long tasks that make the page unresponsive. Such tasks can certainly affect your website's [Interaction to Next Paint (INP)](https://web.dev/articles/inp), so it can be helpful to know when you have work that can be done off of the main thread entirely. Doing so can help create more room for other tasks on the main thread so that user interactions are faster.

This module and the [subsequent demo showing a concrete use case](https://web.dev/learn/performance/web-worker-demo) covers web workers. The demo itself shows how you can use a web worker to perform the work of reading image metadata from a JPEG file off of the main thread—and how you can get that metadata back to the main thread for the user to see.

## How a web worker is launched

A web worker is registered by instantiating the [`Worker` class](https://developer.mozilla.org/docs/Web/API/Worker). When you do so, you specify where the web worker code is located, which the browser loads and subsequently creates a new thread for. The resulting thread is often called a _worker thread_.

```
const myWebWorker = new Worker('/js/my-web-worker.js');
```

In the worker's JavaScript file—`my-web-worker.js` in this case—you can then write code that then runs in a separate worker thread.

## Web worker limitations

Unlike JavaScript that runs on the main thread, web workers lack direct access to the [`window` context](https://developer.mozilla.org/docs/Web/API/Window). and have limited access to the APIs it provides. Web workers are subject to the following constraints:

*   Web workers can't directly access the DOM.
*   Web workers _can_ communicate with the `window` context through a messaging pipeline, meaning that a web worker can _indirectly_ access the DOM in a way.
*   The web worker scope is `self`, rather than `window`.
*   The web worker scope _does_ have access to JavaScript primitives and constructs, as well as APIs such as `fetch` and [a fairly large number of other APIs](https://developer.mozilla.org/docs/Web/API/Web_Workers_API#supported_web_apis).

## How web workers talk to the `window`

It's possible for a web worker to communicate with the main thread's `window` context through a messaging pipeline. This pipeline lets you ferry data to and from the main thread and the web worker. To send data from a web worker to the main thread, you set up a `message` event on the web worker's context (`self`)

```
// my-web-worker.js
self.addEventListener("message", () => {
  // Sends a message of "Hellow, window!" from the web worker:
  self.postMessage("Hello, window!");
});
```

Then in a script in the `window` context on the main thread, you can receive the message from the web worker thread using yet another `message` event:

```
// scripts.js

// Creates the web worker:
const myWebWorker = new Worker('/js/my-web-worker.js');

// Adds an event listener on the web worker instance that listens for messages:
myWebWorker.addEventListener("message", ({ data }) => {
  // Echoes "Hello, window!" to the console from the worker.
  console.log(data);
});
```

The web worker's messaging pipeline is an escape hatch of sorts from the web worker context. Using it, you can send data to the `window` from the web worker that you can use to update the DOM, or perform other work that must be done on the main thread.

## Test your knowledge

What thread does a web worker run on?

Its own thread (also known as a _web worker thread_).

What can a web worker access?

A strict subset of APIs available in the `window` context, including `fetch`.

JavaScript primitives, such as arrays and objects.

The `window` context, but only indirectly.

How can a web worker access the \`window\` context?

Through a messaging pipeline facilitated by the `postMessage` method in the web worker context (`self`).

Directly, by referencing members of the `window` object.

A web worker can't access the `window` by any means.

## Up next: a concrete web worker use case

In [the next module](https://web.dev/learn/performance/web-worker-demo), a concrete web worker use case is detailed and demonstrated. In that module, a web worker is used to fetch a JPEG file from a given URL, and read its [Exif metadata](https://en.wikipedia.org/wiki/Exif) in a web worker. That data is then sent back to the main thread to be displayed to the user.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
