# Video performance  |  web.dev

**Source URL:** [https://web.dev/learn/performance/video-performance?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%2Fvideo-performance](https://web.dev/learn/performance/video-performance?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fperformance%2Fvideo-performance)  
**Last Updated:** 2025-05-23T01:14:25.241Z  
**Extracted:** 2025-05-31 16:58:10

---

# Glitch

In [the previous module](https://web.dev/learn/performance/image-performance), you learned some performance techniques related to images, which are a widely used resource type on the web that can consume significant bandwidth if care is not taken to optimize them and take the user's viewport into consideration.

However, images aren't the only media type commonly seen on the web. Videos are another popular media type often used on web pages. Before looking at some of the possible optimizations, it's important to first understand how the `<video>` element works.

## Video source files

When working with media files, the file you recognize on your operating system (`.mp4`, `.webm`, and others) is called a _container_. A container contains one or more _streams_. In most cases, this would be the video and audio stream.

You can compress each stream using a codec. For example, a `video.webm` could be a [WebM](https://www.webmproject.org/) container containing a video stream compressed using [VP9](https://en.wikipedia.org/wiki/VP9), and an audio stream compressed using [Vorbis](https://en.wikipedia.org/wiki/Vorbis).

Understanding the difference between containers and codecs is helpful, because it helps you to compress your media files using significantly less bandwidth, which leads to lower overall page load times, as well as potentially improving a page's [Largest Contentful Paint (LCP)](https://web.dev/articles/lcp), which is a [user-centric metric](https://web.dev/articles/user-centric-performance-metrics) and one of the three [Core Web Vitals](https://web.dev/articles/vitals).

One way to compress video files involves using [FFmpeg](https://ffmpeg.org/):

```
ffmpeg -i input.mov output.webm
```

The preceding command—though as basic as it gets when using FFmpeg—takes the `input.mov` file and outputs an `output.webm` file using the default FFmpeg options. The preceding command outputs a smaller video file that works in all modern browsers. Tweaking [the video](https://ffmpeg.org/ffmpeg.html#Video-Options) or [audio options FFmpeg offers](https://ffmpeg.org/ffmpeg.html#Audio-Options) could help you to reduce a video's file size even further. For example, if you are using a `<video>` element to replace a GIF, you should remove the audio track:

```
ffmpeg -i input.mov -an output.webm
```

If you want to tweak things a bit further, FFmpeg offers the `-crf` flag when compressing videos without using variable bitrate encoding. `-crf` stands for **Constant Rate Factor**. This is a setting that adjusts the level of compression, and does so by accepting an integer within a given range.

Codecs such as H.264 and VP9 support the `-crf` flag, but its use depends on which codec you're using. For more info, read about [constant rate factor for encoding videos in H.264](https://trac.ffmpeg.org/wiki/Encode/H.264#crf), as well as [constant quality when encoding videos in VP9](https://trac.ffmpeg.org/wiki/Encode/VP9#constantq).

### Multiple formats

When working with video files, specifying multiple formats works as a fallback for browsers that don't support all modern formats.

```
<video>
  <source src="video.webm" type="video/webm">
  <source src="video.mp4" type="video/mp4">
</video>
```

Since [all modern browsers support the H.264 codec](https://caniuse.com/mpeg4), MP4 can be used as the fallback for legacy browsers. The WebM version can use the newer [AV1 codec](https://en.wikipedia.org/wiki/AV1), which is [not yet as widely supported](https://caniuse.com/av1), or the earlier VP9 codec, which is [better supported than AV1](https://caniuse.com/webm), but typically doesn't compress as well as AV1.

## The `poster` attribute

A video's poster image is added using the [`poster` attribute](https://developer.mozilla.org/docs/Web/HTML/Element/video#attr-poster) on the `<video>` element, which hints to users what the video contents may be before playback is initiated:

```
<video poster="poster.jpg">
  <source src="video.webm" type="video/webm">
  <source src="video.mp4" type="video/mp4">
</video>
```

## Autoplay

According to the HTTP Archive, [20% of videos](https://almanac.httparchive.org/en/2022/media#fig-37) across the web include the `autoplay` attribute. `autoplay` is used when a video must be played immediately—such as when used as a video background or as a [replacement for animated GIFs](https://web.dev/articles/replace-gifs-with-videos).

Animated GIFs can be very large, especially if they have many frames with intricate details. It's not uncommon for animated GIFs to consume several megabytes of data, which can be a significant drain on bandwidth better spent for more critical resources. You should generally avoid animated image formats, as `<video>` equivalents are much more efficient for this type of media.

If autoplaying video is a requirement for your website, you can use the `autoplay` attribute directly on the `<video>` element:

```
<!-- This will automatically play a video, but
     it will loop continuously and be muted: -->
<video autoplay muted loop playsinline>
  <source src="video.webm" type="video/webm">
  <source src="video.mp4" type="video/mp4">
</video>
```

By combining the `poster` attribute with the [Intersection Observer API](https://developer.mozilla.org/docs/Web/API/Intersection_Observer_API) you can configure your page to only [download videos once they are within the viewport](https://web.dev/articles/lazy-loading-video#video-gif-replacement). The `poster` image could be a low-quality image placeholder, such as the first frame of the video. Once the video appears in the viewport, the browser begins downloading the video. This could improve load times for content within the initial viewport. On the downside, when using a `poster` image for `autoplay`, your users receive an image that is shown only briefly until the video has loaded and begins playing.

## User-initiated playback

Generally, the browser begins downloading a video file as soon as the HTML parser discovers the `<video>` element. If you have `<video>` elements where the user initiates playback, you probably don't want the video to begin downloading until the user has interacted with it.

You can affect what is downloaded for video resources by using the `<video>` element's [`preload`](https://developer.mozilla.org/docs/Web/HTML/Element/video#attr-preload) attribute:

*   Setting `preload="none"` informs the browser that none of the video's contents should preloaded.
*   Setting `preload="metadata"` only fetches video metadata, such as the video's duration and possibly other cursory information.

Setting `preload="none"` is likely the most desirable case if you're loading videos that users need to initiate playback for.

You can improve the user experience in this case by adding a `poster` image. This gives the user some context on what the video is about. Additionally, if the poster image is your LCP element, you can increase the `poster` image's priority using the `<link rel="preload">` hint along with `fetchpriority="high"`:

```
<link rel="preload" as="image" href="poster.jpg" fetchpriority="high">
```

## Embeds

Given all the complexity in optimizing and serving video content efficiently, it makes sense to want to offload the problem to dedicated video services such as YouTube or Vimeo. Such services optimize the delivery of videos for you, but embedding a video from a third party service can have its own sort of effect on performance, as the embedded video players can often serve a lot of extra resources, such as JavaScript.

Given this reality, third-party video embeds can significantly impact page performance. According to the HTTP Archive, YouTube embeds block the main thread for more than [1.7 seconds](https://almanac.httparchive.org/en/2022/third-parties#fig-8) for the median website. Blocking the main thread for long periods of time is a serious user experience problem that can impact a page's [Interaction to Next Paint (INP)](https://web.dev/articles/inp). However, you can strike a compromise by _not_ loading the embed immediately during the initial page load, and instead create a placeholder for the embed that is replaced by the actual video embed when the user interacts with it.

## Video demos

## Test your knowledge

The order of `<source>` elements inside of a parent `<video>` element does _not_ determine which video resource is ultimately downloaded.

The `<video>` element's `poster` attribute is considered an LCP candidate.

## Up next: Optimize web fonts

Next up in our coverage of optimizing specific resource types is fonts. [Optimizing your website's fonts](https://web.dev/learn/performance/optimize-web-fonts) is something that is often overlooked, but can have a significant impact on your website's overall load speed, and metrics such as LCP and [Cumulative Layout Shift (CLS)](https://web.dev/articles/cls).

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
