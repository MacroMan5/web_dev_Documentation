# Typography  |  web.dev

**Source URL:** [https://web.dev/learn/accessibility/typography?continue=https%3A%2F%2Fweb.dev%2Flearn%2Faccessibility%23article-https%3A%2F%2Fweb.dev%2Flearn%2Faccessibility%2Ftypography](https://web.dev/learn/accessibility/typography?continue=https%3A%2F%2Fweb.dev%2Flearn%2Faccessibility%23article-https%3A%2F%2Fweb.dev%2Flearn%2Faccessibility%2Ftypography)  
**Last Updated:** 2025-05-23T01:16:37.437Z  
**Extracted:** 2025-05-31 16:58:10

---

# Typography  |  web.dev

Creating and designing accessible content is more than just choosing an easy-to-read font. Even with accessible font families, people with low vision, cognitive, language, and learning disabilities may struggle to process the text due to other elements such as font variations, size, spacing, and kerning—to name a few.

This module looks at basic design considerations to make your content more inclusive and reach even more people.

## Typeface

A major factor that can strongly impact copy accessibility is the typeface. Your choice of typeface and style can make or break any page design.

People with reading, learning, and attention disorders like dyslexia and attention-deficit hyperactivity disorder (ADHD), as well as people with low vision, can all benefit when you use accessible typefaces.

### Choose common typefaces

The quickest way to create an accessible design is to choose a common typeface (such as Arial, Times New Roman, Calibri, Verdana, and many others).

Many [typeface studies](http://dyslexiahelp.umich.edu/sites/default/files/good_fonts_for_dyslexia_study.pdf) testing people with disabilities show that common typefaces lead to faster reading speeds and a deeper comprehension level when compared to uncommon typefaces. While common typefaces aren't inherently more accessible than other typefaces, some people with disabilities have an easier time reading them because they have had a lot of experience working with (or around) these typefaces.

In addition to choosing a common typeface, be sure to avoid ornate or handwritten typefaces, as well as ones with only one character case available (for example, only uppercase characters). These specialty typefaces with cursive designs, quirky shapes, or artistic features like thin lines may look nice, but they are much harder for some people with disabilities to read than common typefaces.

  CodePen Embed - Accessible Typography - Typeface  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

### Letter characteristics and kerning

The research on whether [serif or sans serif typefaces are easier to read](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4612630/) is inconclusive, but certain numbers, letters, or combinations can confuse [people with language-based learning and cognitive disabilities](https://www.ncld.org/news/newsroom/the-state-of-ld-understanding-the-1-in-5/). For people with these types of disabilities, every letter and number must be clearly defined and have unique characteristics, so letters are not confused with a numbers.

Common readability offenders are the uppercase `I` (India), lowercase `l` (lettuce), and the number `1`. Likewise, letter pairs like `b` and `d`, `p` and `q`, `f` and `t`, `i` and `j`, `m` and `w`, and `n` and `u` may appear flipped, either left-right or up-down, for some readers.

The copy's readability also decreases when the letter spacing or kerning is too tight. Pay special attention to kerning, especially between the problematic letter pair r/n. Otherwise, words like "yarn" could change to "yam" or "stern" to "stem," entirely changing the meaning of the copy.

Open source typeface collections like [Google Fonts](https://fonts.google.com/) can aid you in selecting the most inclusive typeface for your next design. If you use Adobe products, you can embed accessible font families from foundry partners directly into your designs—this includes select [Google Fonts](https://fonts.adobe.com/foundries/google).

  CodePen Embed - Accessible Typography - Letter characteristics  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

When you are looking for your next typeface, pay particular attention to the following:

*   Use common fonts whenever possible.
*   Avoid using elaborate or handwritten fonts and those with only one character case.
*   Pick a typeface with unique characteristics—paying special attention to the uppercase I, lowercase l, and 1.
*   Review certain letter combinations to be sure they are not an exact mirror image of one another.
*   Check the kerning, especially between the r and n letter pair.

### Font size and typographic styling

People often assume that picking out an accessible font family is all there is to creating inclusive content, but it is also important to consider the [font size](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html) and how the text is styled on a page.

For example, people with low vision or color blindness may be unable to read some of the copy if it's too small, using an AT—like browser zoom to read the copy. Other users, such as those with dyslexia or reading disorders, may have trouble reading italic text. Screen readers often ignore styling methods, such as bold and italics, so the intent of these styles is not conveyed to blind or low-vision users.

Don't

h2 {font-size: 16px;}

Since you cannot predict what every user's needs are, when adding fonts to your websites and web applications, be sure to consider the following guidelines:

*   Base font sizes should be defined with a relative value (%, rem, or em) to allow for resizing.
*   Limit the number of typeface variations like color, **bold**, ALL CAPS, and _italics_ to increase readability. Instead, use methods to emphasize words in your copy, such as asterisks, dashes, or highlighting an individual word.
*   Use markup instead of text on images whenever possible. Screen readers cannot read embedded text on images (without extra code added), and embedded text can also become pixelated when magnified by low-vision users.

## Structure and layout

While typeface, font size, and typographic styling are important to accessible typography, the [structure](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html) and [layout](https://www.w3.org/WAI/WCAG21/Understanding/reflow) of copy on a page can be equally important to a user's understanding.

Complex layouts can be a real barrier for people with low vision, reading disabilities, and the [6.1 million people in the US with ADHD](https://www.cdc.gov/adhd/data/index.html). These types of disabilities make it more difficult for people to keep their place and follow the flow of the copy due to the lack of clear linear pathways, missing headings, and ungrouped elements.

An important aspect of accessible layout designs is making critical elements distinct from one another and grouping similar elements together. If the elements are too close, it can be difficult to tell where one element begins and ends, especially if they have similar styling.

Think about your copy as a collection of individual bullet points on an outline. This will help you plan out the overall page structure and enable you to use headings, subheadings, and lists whenever appropriate.

  CodePen Embed - Accessible Typography - Structure  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

### Spacing

[Paragraph, sentence, and word spacing](https://www.w3.org/WAI/WCAG22/Understanding/text-spacing.html) helps readers retain their focus on the copy and adds to the page's overall visual understanding. Long lines of copy can be a barrier for readers with disabilities, as they have trouble keeping their place and following the flow of the copy.

A narrow block of copy makes it easier for readers to continue to the next line.

  CodePen Embed - Accessible Typography - Spacing  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

### Content alignment

Another frustration for many people with disabilities is reading justified copy. The uneven spacing between words in justified copy can cause "rivers of space" to form down the page, making the copy difficult to read.

Text justification can also cause words to be either bunched together or stretched in unnatural ways, so readers can find it difficult to locate word boundaries.

  CodePen Embed - Accessible Typography - Text alignment  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### External CSS

This Pen doesn't use any external CSS resources.

### External JavaScript

This Pen doesn't use any external JavaScript resources.

Thankfully, there are clear guidelines on spacing and tools such as [Good Line-Height](http://thegoodlineheight.com/) and the [Golden Ratio Calculator](https://grtcalculator.com/) to help make our copy more accessible. Incorporating these guidelines helps people with attention-deficit disorders, reading, and vision-based disabilities focus more on the copy and less on the layout.

### Best practices for structure and layout

When considering structure and layout, be sure to:

*   Use elements like headings, subheadings, lists, numbers, quote blocks, and other visual groupings to break the page into sections.
*   Use clearly defined paragraphs, sentences, and word spacing.
*   Build columns of copy that are smaller than 80 characters in width (40 characters for logograms).
*   Avoid justified paragraph alignment, which creates "rivers of space" within the copy.

## Accessible typography takeaways

Accessible typography can be boiled down to common-sense design choices based on your knowledge of your users' needs. Keeping this module in mind as you design and build out your content will go a long way toward helping you communicate clearly with the greatest number of people.

## Check your understanding

Test your knowledge of typographic accessibility.

For readable copy, I should always use high-contrast between my copy and background.

What fonts are the best for accessibility?

System fonts like Arial and Verdana.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
