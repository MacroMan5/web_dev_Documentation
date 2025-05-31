# A concrete web worker use case  |  web.dev

**Source URL:** [https://web.dev/learn/performance/web-worker-demo?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%2Fweb-worker-demo](https://web.dev/learn/performance/web-worker-demo?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%2Fweb-worker-demo)  
**Last Updated:** 2025-05-23T01:15:12.042Z  
**Extracted:** 2025-05-31 16:58:10

---

# A concrete web worker use case | web.dev

In the last module, an [overview of web workers](https://web.dev/learn/performance/web-worker-overview) was given. Web workers can improve input responsiveness by moving JavaScript off of the main thread to separate web worker threads, which can help improve your website's [Interaction to Next Paint (INP)](https://web.dev/articles/inp) when you have work that doesn't need direct access to the main thread. However, an overview alone isn't sufficient, and in this module, a concrete use case for a web worker is offered.

One such use case could be a website that needs to strip [Exif metadata](https://en.wikipedia.org/wiki/Exif) from an image—this isn't such a far-fetched concept. In fact, websites like Flickr offer users a way to view Exif metadata in order to learn technical details about the images they host, such as the color depth, camera make and model, and other data.

However, the logic for fetching an image, converting it to an [`ArrayBuffer`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer), and extracting the Exif metadata could be potentially expensive if done entirely on the main thread. Thankfully, the web worker scope allows for this work done off of the main thread. Then, using the web worker's messaging pipeline, the Exif metadata is transmitted back to the main thread as an HTML string, and displayed to the user.

### What the main thread looks like without a web worker

First, observe what the main thread looks like when we do this work without a web worker. To do this, perform the following steps:

1.  Open a new tab in Chrome, and open its DevTools.
2.  Open the **performance panel**.
3.  Navigate to [https://exif-worker.glitch.me/without-worker.html](https://exif-worker.glitch.me/without-worker.html).
4.  In the performance panel, click **Record** at the upper right hand corner of the DevTools pane.
5.  Paste [this image link](https://upload.wikimedia.org/wikipedia/commons/5/59/Vespula_germanica_Richard_Bartz.jpg)—or another one of your choosing that contains Exif metadata—in the field and click the **Get that JPEG!** button.
6.  Once the interface populates with Exif metadata, click **Record** again to stop recording.

![The performance profiler showing the image metadata extractor app's activity occurring entirely on the main thread. The there are two substantial long tasks—one that runs a fetch to get the requested image and decode it, and another that extracts the metadata from the image.](https://web.dev/static/learn/performance/web-worker-demo/image/fig-1.opt.png)

Main thread activity in the image metadata extractor app. Note that all of the activity occurs on the main thread.

Note that—aside from other threads that may be present, such as rasterizer threads and so on—everything in the app occurs on the main thread. On the main thread, the following happens:

1.  The form takes the input and dispatches a `fetch` request to get the initial portion of the image containing the Exif metadata.
2.  The image data is converted into an `ArrayBuffer`.
3.  The [`exif-reader`](https://www.npmjs.com/package/exif-reader) script is used to extract the Exif metadata from the image.
4.  The metadata is scraped to construct an HTML string, which then populates the metadata viewer.

Now contrast that with an implementation of the same behavior—but using a web worker!

### What the main thread looks like _with_ a web worker

Now that you've seen what things look like to extract the Exif metadata from a JPEG file on the main thread, take a look at what it looks like when a web worker is in the mix:

1.  Open a another tab in Chrome, and open its DevTools.
2.  Open the **performance panel**.
3.  Navigate to [https://exif-worker.glitch.me/with-worker.html](https://exif-worker.glitch.me/with-worker.html).
4.  In the performance panel, click the **record button** at the upper right hand corner of the DevTools pane.
5.  Paste [this image link](https://upload.wikimedia.org/wikipedia/commons/5/59/Vespula_germanica_Richard_Bartz.jpg) in the field and click the **Get that JPEG!** button.
6.  Once the interface populates with Exif metadata, click the **record button** again to stop recording.

![The performance profiler showing the image metadata extractor app's activity occurring on both the main thread and a web worker thread. While there are still long tasks on the main thread, they are substantially shorter, with the image fetching/decoding and metadata extraction occurring entirely on a web worker thread. The only main thread work involves passing data to and from the web worker.](https://web.dev/static/learn/performance/web-worker-demo/image/fig-2.opt.png)

Main thread activity in the image metadata extractor app. Note that there is an additional web worker thread where most of the work is done.

This is the power of a web worker. Rather than doing _everything_ on the main thread, everything but populating the metadata viewer with HTML is done on a separate thread. This means that the main thread is freed up to do other work.

Perhaps the biggest advantage here is that, unlike the version of this app that doesn't use a web worker, the `exif-reader` script isn't loaded on the main thread, but rather on the web worker thread. This means that the cost of downloading, parsing, and compiling the `exif-reader` script takes place off the main thread.

Now to dive into the web worker code that makes this all possible!

## A look at the web worker code

It's not enough to see the difference a web worker makes, it also helps to understand—at least in this case—what that code looks like so you know what's possible in the web worker scope.

Start with the main thread code that needs to occur before the web worker can enter the picture:

```
// scripts.js

// Register the Exif reader web worker:
const exifWorker = new Worker('/js/with-worker/exif-worker.js');

// We have to send image requests through this proxy due to CORS limitations:
const imageFetchPrefix = 'https://res.cloudinary.com/demo/image/fetch/';

// Necessary elements we need to select:
const imageFetchPanel = document.getElementById('image-fetch');
const imageExifDataPanel = document.getElementById('image-exif-data');
const exifDataPanel = document.getElementById('exif-data');
const imageInput = document.getElementById('image-url');

// What to do when the form is submitted.
document.getElementById('image-form').addEventListener('submit', event => {
  // Don't let the form submit by default:
  event.preventDefault();

  // Send the image URL to the web worker on submit:
  exifWorker.postMessage(`${imageFetchPrefix}${imageInput.value}`);
});

// This listens for the Exif metadata to come back from the web worker:
exifWorker.addEventListener('message', ({ data }) => {
  // This populates the Exif metadata viewer:
  exifDataPanel.innerHTML = data.message;
  imageFetchPanel.style.display = 'none';
  imageExifDataPanel.style.display = 'block';
});
```

This code runs on the main thread, and sets up the form to send the image URL to the web worker. From there, the web worker code starts with an [`importScripts`](https://developer.mozilla.org/docs/Web/API/WorkerGlobalScope/importScripts) statement that loads the external `exif-reader` script, and then sets up the messaging pipeline to the main thread:

```
// exif-worker.js

// Import the exif-reader script:
importScripts('/js/with-worker/exifreader.js');

// Set up a messaging pipeline to send the Exif data to the `window`:
self.addEventListener('message', ({ data }) => {
  getExifDataFromImage(data).then(status => {
    self.postMessage(status);
  });
});
```

This bit of JavaScript sets up the messaging pipeline so that when the user submits the form with a URL to a JPEG file, the URL arrives in the web worker. From there, this next bit of code extracts the Exif metadata from the JPEG file, builds an HTML string, and sends that HTML back to the `window` to eventually be displayed to the user:

```
// Takes a blob to transform the image data into an `ArrayBuffer`:
// NOTE: these promises are simplified for readability, and don't include
// rejections on failures. Check out the complete web worker code:
// https://glitch.com/edit/#!/exif-worker?path=js%2Fwith-worker%2Fexif-worker.js%3A10%3A5
const readBlobAsArrayBuffer = blob => new Promise(resolve => {
  const reader = new FileReader();

  reader.onload = () => {
    resolve(reader.result);
  };

  reader.readAsArrayBuffer(blob);
});

// Takes the Exif metadata and converts it to a markup string to
// display in the Exif metadata viewer in the DOM:
const exifToMarkup = exif => Object.entries(exif).map(([exifNode, exifData]) => {
  return `
    <details>
      <summary>
        <h2>${exifNode}</h2>
      </summary>
      <p>${exifNode === 'base64' ? `<img src="data:image/jpeg;base64,${exifData}">` : typeof exifData.value === 'undefined' ? exifData : exifData.description || exifData.value}</p>
    </details>
  `;
}).join('');

// Fetches a partial image and gets its Exif data
const getExifDataFromImage = imageUrl => new Promise(resolve => {
  fetch(imageUrl, {
    headers: {
      // Use a range request to only download the first 64 KiB of an image.
      // This ensures bandwidth isn't wasted by downloading what may be a huge
      // JPEG file when all that's needed is the metadata.
      'Range': `bytes=0-${2 ** 10 * 64}`
    }
  }).then(response => {
    if (response.ok) {
      return response.clone().blob();
    }
  }).then(responseBlob => {
    readBlobAsArrayBuffer(responseBlob).then(arrayBuffer => {
      const tags = ExifReader.load(arrayBuffer, {
        expanded: true
      });

      resolve({
        status: true,
        message: Object.values(tags).map(tag => exifToMarkup(tag)).join('')
      });
    });
  });
});
```

It's a bit to read, but this is also a fairly involved use case for web workers. However, the results are worth the work, and not just limited to this use case. You can use web workers for all sorts of things, such as isolating `fetch` calls and processing responses, processing large amounts of data without blocking the main thread—and that's just for starters.

When improving the performance of your web applications, start thinking about anything that can be reasonably done in a web worker context. The gains could be significant, and can lead to an overall better user experience for your website.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
