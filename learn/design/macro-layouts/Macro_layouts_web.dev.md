# Macro layouts  |  web.dev

**Source URL:** [https://web.dev/learn/design/macro-layouts?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%2Fmacro-layouts](https://web.dev/learn/design/macro-layouts?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fdesign%2Fmacro-layouts)  
**Last Updated:** 2025-05-23T00:54:12.356Z  
**Extracted:** 2025-05-31 16:58:10

---

# Macro layouts  |  web.dev

Macro layouts

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

Macro layouts describe the larger, page-wide organization of your interface.

![A wireframe of a two column layout, next to the same layout as one column for a narrow view.](https://web.dev/static/learn/design/macro-layouts/image/a-wireframe-a-column-la-a517dae97f715.jpeg)

Before applying any layout, you should make sure that the flow of your content makes sense. This single column default ordering is what smaller screens will get.

```
<body>
  <header>…</header>
  <main>
    <article>…</article>
    <aside>…</aside>
  </main>
  <footer>…</footer>
</body>
```

  CodePen Embed - LearnDesign: Macro "A web page"  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

When you arrange these individual page-level components, you're designing a macro layout: a high-level view of your page. Using media queries, you can supply rules in CSS describing how this view should adjust to different screen sizes.

## Grid

[CSS grid](https://web.dev/learn/css/grid) is an excellent tool for applying a layout to your page. In the example above, say you want a two-column layout once there's enough screen width available. To apply this two-column layout once the browser is wide enough, use a media query to define the grid styles above a specified breakpoint.

```
@media (min-width: 45em) {
  main {
    display: grid;
    grid-template-columns: 2fr 1fr;
  }
}
```

  CodePen Embed - LearnDesign: Macro "A web page with layout"  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Flexbox

For this specific layout, you could also use [flexbox](https://web.dev/learn/css/flexbox). The styles would look like this:

```
@media (min-width: 45em) {
  main {
    display: flex;
    flex-direction: row;
  }

  main article {
    flex: 2;
  }

  main aside {
    flex: 1;
  }
}
```

  CodePen Embed - LearnDesign: Macro "A web page with flexbox layout"  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

However, the flexbox version requires more CSS. Each column has a separate rule to describe how much space it should take up. In the grid example, that same information is encapsulated in one rule for the containing element.

You might not always need to use a media query. Media queries work fine when you're applying changes to a few elements, but if the layout needs to be updated a lot, your media queries could get out of hand with lots of breakpoints.

Say you've got a page full of card components. The cards are never wider than `15em`, and you want to put as many cards on one line as will fit. You could write media queries with breakpoints of `30em`, `45em`, `60em`, and so on, but that's quite tedious and difficult to maintain.

Instead, you can apply rules so that the cards themselves automatically take up the right amount of space.

```
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(15em, 1fr));
  grid-gap: 1em;
}
```

  CodePen Embed - LearnDesign: Macro "Cards"  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

You can achieve a similar layout with flexbox. In this case, if there are not enough cards to fill the final row, the remaining cards will stretch to fill the available space rather than lining up in columns. If you want to line up rows and columns, then use grid.

```
.cards {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 1em;
}
.cards .card {
  flex-basis: 15em;
  flex-grow: 1;
}
```

  CodePen Embed - LearnDesign: Macro "Flexbox cards"  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

By applying some smart rules in flexbox or grid, it's possible to design dynamic macro layouts with minimal CSS and without any media queries. That's less work for you—you're making the browser do the calculations instead. To see some examples of modern CSS layouts that are fluid without requiring media queries, see [1linelayouts.com](https://1linelayouts.glitch.me/).

### Check your understanding

Test your knowledge of macro layouts.

Which sentence best describes macro layouts?

Low level layouts which cover small amounts of the screen.

High level layouts which cover large amounts of the screen.

When a design uses flexbox or grid.

Layouts that contain other layouts.

Macro layouts always use media queries to adapt to different screen sizes?

Now that you've got some ideas for page-level macro layouts, turn your attention to the components within the page. This is the realm of [micro layouts](https://web.dev/learn/design/micro-layouts).

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
