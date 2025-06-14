# Internationalization  |  web.dev

**Source URL:** [https://web.dev/learn/design/internationalization?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%2Finternationalization](https://web.dev/learn/design/internationalization?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%2Finternationalization)  
**Last Updated:** 2025-05-23T00:54:11.039Z  
**Extracted:** 2025-05-31 16:58:10

---

# Internationalization  |  web.dev

The World Wide Web is available to everyone in the world—it's right there in the name! That means that your website is potentially available to anyone who has access to the internet, regardless of where they are, what device they're using, or what languages they speak.

The goal of responsive design is to make your content available to everyone. Applying that same philosophy to human languages is the driving force behind internationalization—preparing your content and designs for an international audience.

## Logical properties

English is written from left to right and top to bottom, but not all languages are written this way. Some languages like Arabic and Hebrew read from right to left, and some Japanese typefaces read vertically instead of horizontally. To accommodate these writing modes, logical properties were introduced in CSS.

If you write CSS, you may have used directional keywords like "left", "right", "top", and "bottom." Those keywords refer to the physical layout of the user's device.

[Logical properties](https://web.dev/learn/css/logical-properties), on the other hand, refer to the edges of a box as they relate to the flow of content. If the writing mode changes, CSS written with logical properties will update accordingly. That's not the case with directional properties.

Whereas the directional property `margin-left` always refers to the margin on the left side of a content box, the logical property `margin-inline-start` refers to the margin on the left side of a content box in a left-to-right language, and the margin on the right side of a content box in a right-to-left language.

In order for your designs to adapt to different writing modes, avoid directional properties. Use logical properties instead.

Don't

.byline {
  text-align: right;
}

Do

.byline {
  text-align: end;
}

When CSS has a specific directional value like `left` or `right`, there's a corresponding logical property. Where once we had `margin-left` now we also have `margin-inline-start`.

In a language like English where text flows from left to right, `inline-start` corresponds to "left" and `inline-end` corresponds to "right".

Likewise, in a language like English where the text is written from top to bottom, `block-start` corresponds to "top" and `block-end` corresponds to "bottom."

![Latin, Hebrew and Japanese are shown rendering placeholder text within a device frame. Arrows and colors follow the text to help associate the 2 directions of block and inline.](https://web.dev/static/learn/design/internationalization/image/latin-hebrew-japanese-a-538b56c52363b.webp)

If you use logical properties in your CSS, you can use the same stylesheet for translations of your pages. Even if your pages are translated into languages written from right to left or bottom to top, your design will adjust accordingly. You don't need to make separate designs for each language. By using logical properties, your design will respond to every writing mode. That means your design can reach more people without you having to spend time making separate designs for every language.

Modern CSS layout techniques like [grid](https://web.dev/learn/css/grid) and [flexbox](https://web.dev/learn/css/flexbox) use logical properties by default. If you think in terms of `inline-start` and `block-start` instead of `left` and `top` then you'll find these modern techniques easier to understand.

Take a common pattern like [an icon next to some text](https://web.dev/learn/css/logical-properties#solving_the_icon_issue) or a label next to a form field. Instead of thinking "the label should have a margin on the right," think "the label should have a margin on the end of its inline axis."

Don't

label {
  margin-right: 0.5em;
}

Do

label {
  margin-inline-end: 0.5em;
}

  CodePen Embed - LearnDesign: i18n "Left-to-right form"  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

If that page is translated into a right-to-left language, the styles won't need to be updated. You can mimic the effect of seeing your pages in a right-to-left language by using the `dir` attribute on your `html` element. A value of `ltr` means "left to right." A value of "rtl" means "right to left."

  CodePen Embed - LearnDesign: i18n "Right-to-left form"  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

If you'd like to experiment with all the permutations of document directions (the block axis) and writing modes (the inline axis), here's [an interactive demonstration](https://codepen.io/argyleink/pen/vYNwbgM).

  CodePen Embed - International Layouts w/ Intrinsic & Logical Properties  

[![](https://assets.codepen.io/2585/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1580330623&width=256)](https://codepen.io/argyleink)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

## Identify page language

It's a good idea to identify the language of your page by using the `lang` attribute on the `html` element.

```
<html lang="en">
```

That example is for a page in English. You can be even more specific. Here's how you declare that a page is using US English:

```
<html lang="en-us">
```

Declaring the language of your document is useful for search engines. It's also useful for assistive technologies like screen readers and voice assistants. By providing language metadata you're helping these kinds of speech synthesizers pronounce your content correctly.

The `lang` attribute can go on any HTML element, not just `html`. If you switch languages in your web page, indicate that change. In this case, one word is in German:

```
<p>I felt some <span lang="de">schadenfreude</span>.</p>
```

## Identify a linked document's language

There's another attribute called `hreflang` which you can use on links. The `hreflang` takes the same language code notation as the `lang` attribute and describes the linked document's language. If there's a translation of your entire page available in German, link to it like this:

```
<a href="/path/to/german/version" hreflang="de">German version</a>
```

If you use text in German to describe the link to the German version, use both `hreflang` and `lang`. Here, the text "Deutsche Version" is marked up as being in the German language, and the destination link is also marked up as being in German:

```
<a href="/path/to/german/version" hreflang="de" lang="de">Deutsche Version</a>
```

You can also use the `hreflang` attribute on the `link` element. This goes in the `head` of your document:

```
<link href="/path/to/german/version" rel="alternate" hreflang="de">
```

But unlike the `lang` attribute, which can go on any element, `hreflang` can only be applied to `a` and `link` elements.

## Consider internationalization in your design

When you're designing websites that will be translated into other languages and writing modes, think about these factors:

*   Some languages, like German, have long words in common usage. Your interface needs to adapt to these words so avoid designing narrow columns. You can also [use CSS to introduce hyphens](https://developer.mozilla.org/docs/Web/CSS/hyphens).
*   Make sure your `line-height` values can accommodate characters like accents and other diacritics. Lines of text that look fine in English might overlap in a different language.
*   If you're using a web font, make sure it has a range of characters broad enough to cover the languages you'll be translating into.
*   Don't create images that have text in them. If you do, you'll have to create separate images for each language. Instead, separate the text and the image, and use CSS to overlay the text on the image.

## Think internationally

Attributes like `lang` and `hreflang` make your HTML more meaningful for internationalization. Likewise, logical properties make your CSS more adaptable.

If you're used to thinking in terms of `top`, `bottom`, `left`, and `right`, it might be hard to start thinking of `block start`, `block end`, `inline start` and `inline end` instead. But it's worth it. Logical properties are key to creating truly responsive layouts.

### Check your understanding

Test your knowledge of internationalization.

In English, the physical `right` side of a box, is logically which side?

Which attribute should you add to your HTML to make it more meaningful for internationalization?

Next, you'll learn how to approach page-level layouts, also known as [macro layouts](https://web.dev/learn/design/macro-layouts).

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
