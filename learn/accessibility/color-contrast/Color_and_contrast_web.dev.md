# Color and contrast  |  web.dev

**Source URL:** [https://web.dev/learn/accessibility/color-contrast?continue=https%3A%2F%2Fweb.dev%2Flearn%2Faccessibility%23article-https%3A%2F%2Fweb.dev%2Flearn%2Faccessibility%2Fcolor-contrast](https://web.dev/learn/accessibility/color-contrast?continue=https%3A%2F%2Fweb.dev%2Flearn%2Faccessibility%23article-https%3A%2F%2Fweb.dev%2Flearn%2Faccessibility%2Fcolor-contrast)  
**Last Updated:** 2025-05-23T01:16:30.256Z  
**Extracted:** 2025-05-31 16:58:10

---

# Color and contrast | web.dev

Have you ever tried to read text on a screen and found it difficult to read due to the color scheme or struggled to see the screen in a very bright or low-light environment? Or maybe you are someone with a more permanent color vision issue, like the estimated [300 million people with color blindness](https://www.colourblindawareness.org/colour-blindness/) or the [253 million people with low vision](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5820628/)?

As a designer or developer, you need to understand how people perceive color and contrast, whether temporary, situationally, or permanently. This helps you best support their visual needs.

This module will introduce you to some accessible color and contrast fundamentals.

## Perceive color

![An eye viewing the color wheel.](https://web.dev/static/learn/accessibility/color-contrast/image/an-eye-viewing-color-whe-358cdaa2d25c.png)

Did you know that objects don't possess color but reflect wavelengths of light? When you see color, your eyes receive and process those wavelengths and convert them to colors.

When it comes to digital accessibility, we talk about these wavelengths in terms of hue, saturation, and lightness (HSL). The HSL model was created as an alternative to the RGB color model and more closely aligns with how a human perceives color.

_Hue_ is a qualitative way to describe a color, such as red, green, or blue, where each hue has a specific spot on the color spectrum with values ranging from 0 to 360, with red at 0, green at 120, and blue at 240.

  CodePen Embed - Accessible Color - Hue  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

Saturation is the intensity of a color, measured in percentages ranging from 0% to 100%. A color with full saturation (100%) would be very vivid, while a color with no saturation (0%) would be grayscale or black and white.

  CodePen Embed - Accessible Color - Saturation  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

Lightness is a color's light or dark character, measured in percentages ranging from 0% (black) to 100% (white).

  CodePen Embed - Accessible Color - Lightness  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

## Measure color contrast

To help support people with various visual disabilities, the WAI group created a [color contrast formula](https://www.w3.org/TR/WCAG22/#dfn-contrast-ratio) to ensure [enough contrast exists](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html) between the text and its background. When these color contrast ratios are followed, people with moderately low vision can read text on the background without needing contrast-enhancing assistive technology.

Take a look at images with a vibrant color palette and compare how that image would appear to those with specific forms of color blindness.

On the left, the image shows rainbow sand with purple, red, orange, yellow, aqua green, light blue, and dark blue colors. On the right is a brighter, multicolored rainbow pattern.

### Deuteranopia

[Deuteranopia](https://www.color-blindness.com/deuteranopia-red-green-color-blindness/) (commonly known as green blind) occurs in 1% to 5% of males, 0.35% to 0.1% of females.

People with Deuteranopia have a reduced sensitivity to green light. This color blindness filter simulates what this type of color blindness might look like.

### Protanopia

[Protanopia](https://www.color-blindness.com/protanopia-red-green-color-blindness/) (commonly known as red blind) occurs in 1.01% to 1.08% of males and 0.02% of 0.03% of females.

People with Protanopia have a reduced sensitivity to red light. This color blindness filter simulates what this type of color blindness might look like.

### Achromatopsia or Monochromatism

[Achromatopsia or Monochromatism](https://www.color-blindness.com/2007/07/20/monochromacy-complete-color-blindness/) (or complete color blindness) occurs very, very rarely.

People with Achromatopsia or Monochromatism have almost no perception of red, green, or blue light. This color blindness filter simulates what this type of color blindness might look like.

### Calculate color contrast

The color contrast formula uses the [relative luminance](https://www.w3.org/TR/WCAG/#dfn-relative-luminance) of colors to help determine contrast, which can range from 1 to 21. This formula is often shortened to `[color value]:1`. For example, pure black against pure white has the largest color contrast ratio at `21:1`.

```
(L1 + 0.05) / (L2 + 0.05)
L1 is the relative luminance of the lighter color
L2 is the relative luminance of the darker colors
```

Regular-sized text, including images of text, must have a color contrast ratio of `4.5:1` to pass the [minimum WCAG requirements for color](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html). Large-sized text and essential icons must have a color contrast ratio of `3:1`. Large-sized text is characterized by being at least 18pt / 24px or 14pt / 18.5px bolded. Logos and decorative elements are exempt from these color contrast requirements.

Thankfully, no advanced math is required as there are a lot of tools that will do the color contrast calculations for you. Tools like [Adobe Color](https://color.adobe.com/create/color-accessibility), [Color Contrast Analyzer](https://www.tpgi.com/color-contrast-checker/), [Leonardo](https://leonardocolor.io/), and [Chrome's DevTools color picker](https://developer.chrome.com/docs/devtools/accessibility/reference#contrast) can quickly tell you the color contrast ratios and offer suggestions to help create the most inclusive color pairs and palettes.

  CodePen Embed - Accessible Color - Color contrast ratios  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Using color

Without good color contrast levels in place, words, icons, and other graphical elements are [hard to discover](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html), and the design can quickly become inaccessible. But it's also important to pay attention to [how the color is used](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html) on the screen, as you cannot use color alone to convey information, actions, or distinguish a visual element.

For example, if you say, "[click the green button to continue](https://www.w3.org/WAI/WCAG22/Understanding/sensory-characteristics.html)," but omit any additional content or identifiers to the button, it would be difficult for people with certain types of colorblindness to know which button to click. Similarly, many graphs, charts, and tables use color alone to convey information. Adding another identifier, like a pattern, text, or icon, is crucial to help people understand the content.

Reviewing your digital products in grayscale is a good way to detect potential color issues quickly.

  CodePen Embed - Accessible Color - Color in context  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Beyond checking for color contrast ratios and the use of color on your screen, you should consider applying the increasingly popular and supported [media queries](https://web.dev/learn/design/media-features#preferences) that offer the users more control over what is displayed on the screen.

For example, using the [`@prefers-color-scheme`](https://drafts.csswg.org/mediaqueries-5/#descdef-media-prefers-color-scheme) media query, you can create a dark theme, which can be helpful to people with [photophobia](https://w3c.github.io/low-vision-a11y-tf/requirements.html#light-and-glare-sensitivity) or light sensitivity. You could also build a high contrast theme with [`@prefers-contrast`](https://drafts.csswg.org/mediaqueries-5/#descdef-media-prefers-contrast), which supports people with color deficiencies and [contrast sensitivity](https://w3c.github.io/low-vision-a11y-tf/requirements.html#contrast-sensitivity).

### Prefers color scheme

The media query `@prefers-color-scheme` allows users to choose a light or dark-themed version of the website or app they are visiting. You can see this theme change in action by changing your light or dark preference settings and navigating to a browser that supports this media query. Review the [Mac](https://support.apple.com/en-us/HT208976) and [Windows](https://blogs.windows.com/windowsexperience/2016/08/08/windows-10-tip-personalize-your-pc-by-enabling-the-dark-theme/) instructions for dark mode.

![](https://web.dev/static/learn/accessibility/color-contrast/image/mac-settings-ui-e918a99520999.png)

macOS general settings for appearance.

  CodePen Embed - Accessible Color - @prefers-color-scheme  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Prefers contrast

The [`@prefers-contrast`](https://developer.mozilla.org/docs/Web/CSS/@media/prefers-contrast) media query checks the user's OS settings to see if high contrast is toggled on or off. You can see this theme change in action by changing your contrast preference settings and navigating to a browser that supports this media query ([Mac](https://support.apple.com/lv-lv/guide/mac-help/unac089/mac) and [Windows](https://support.microsoft.com/windows/change-color-contrast-in-windows-fedc744c-90ac-69df-aed5-c8a90125e696) contrast mode settings).

  CodePen Embed - Accessible Color - @prefers-contrast  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Layer media queries

You can use multiple color-focused media queries to give your users even more choices. In this example, we stacked `@prefers-color-scheme` and `@prefers-contrast` together.

  CodePen Embed - Accessible Color - Multiple media queries  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Check your understanding

Test your knowledge of color and contrast

Color alone isn't a sufficient identifier for documentation. What else will help readers identify UI elements?

All of the answers are correct

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
