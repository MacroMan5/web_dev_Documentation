# Image formats: PNG  |  web.dev

**Source URL:** [https://web.dev/learn/images/png?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fimages%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fimages%2Fpng](https://web.dev/learn/images/png?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fimages%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fimages%2Fpng)  
**Last Updated:** 2025-05-23T00:53:10.640Z  
**Extracted:** 2025-05-31 16:58:10

---

# Image formats: PNG  |  web.dev

Image formats: PNG

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

There are a few things that set PNG (Portable Network Graphics) apart from other formats, though as it was intended to be a replacement for GIF (due to patent disputes long, long ago) it is similar to GIF in several ways. PNG also uses lossless compression, meaning that the image data will be _compressed_ without any loss of visual fidelity. An image's color palette may be quantized—an “indexed color”, with PNG making use of a palette limited to 256 colors, just like GIF. A far more common “truecolor” PNG can contain many, many more colors—up to 16 million.

PNG and GIF both support transparency, though with a major difference. GIF treats transparency as a binary proposition—a pixel is either an opaque color, or fully transparent. PNG supports “alpha channel” transparency, meaning that each pixel can be set to a level of transparency between 0 (fully transparent) and 255 (fully opaque).

![Two pink flowers showing two levels of transparency.](https://web.dev/static/learn/images/png/image/two-pink-flowers-showing-7d623e613e869.png)

In practical terms, the lack of substantial quantization and lossless compression mean that saving an image as a PNG will never result in a drop in visual quality. However, this almost invariably results in excessively large file sizes compared to more modern web-friendly encodings. The transfer size of a PNG means they are almost never the right choice for photographic content.

![Comparison of JPEG and PNG.](https://web.dev/static/learn/images/png/image/comparison-jpeg-png-187c35c39e0ec.png)

PNG was more commonplace in years past largely for a single use case, as the only raster encoding that supported semi-transparency. Today, PNG should only be considered for simple artwork that requires semi-transparency—a company logo containing a drop shadow, for example—and should be compared carefully to the more modern formats that support semi-transparency, such as WebP.

Much like GIF, PNG was designed to solve use cases that are frequently better served by SVG in terms of both scalability and file size. For that reason, you'll sometimes see PNG used as the fallback version of UI elements in the vanishingly small number of browsers that don't support SVG, though these are increasingly rare.

![PNG and SVG comparison.](https://web.dev/static/learn/images/png/image/png-svg-comparison-8054fcfae1d6d.png)

In practical terms, PNG is a sound choice for maintaining a manageable-sized “canonical” version of a source image, saved in your local development environment or committed to a project repository in case future versions of that image need to be edited or re-saved in alternate formats.

It is worth noting, however, that even though encodings are standardized, different editing tools have different methods of performing that encoding—some much more efficient than others. Before transferring a PNG in any context, be sure to run your files through a tool like [Squoosh](https://squoosh.app/) or [ImageOptim](https://imageoptim.com/).

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
