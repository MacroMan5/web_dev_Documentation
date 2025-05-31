# Transitions  |  web.dev

**Source URL:** [https://web.dev/learn/css/transitions?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Ftransitions](https://web.dev/learn/css/transitions?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fcss%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fcss%2Ftransitions)  
**Last Updated:** 2025-05-23T01:07:11.546Z  
**Extracted:** 2025-05-31 16:58:10

---

# Transitions  |  web.dev

##### [The CSS Podcast - 044: Transitions](https://thecsspodcast.libsyn.com/044-transitions)

When interacting with a website, you might notice that many elements have _state_. For example, dropdowns can be in opened or closed states. Buttons might change color when focused or hovered. Modals appear and disappear.

By default, CSS switches the style of these states instantly.

Using CSS transitions, we can interpolate between the initial state and the target state of the element. The transition between the two enhances the user experience by providing visual direction, support, and hints about the cause and effect of the interaction.

  CodePen Embed - Learn CSS: Transitions - instant vs transitioned (no button)  

Live

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Transition properties

To use transitions in CSS, you can use the various transition properties or the `transition` shorthand property.

### transition-property

The [`transition-property`](https://developer.mozilla.org/docs/Web/CSS/transition-property) property specifies which style(s) to transition.

```
.my-element {
  transition-property: background-color;
}
```

The `transition-property` accepts one or more CSS property names in a comma-separated list.

Optionally, you may use `transition-property: all` to indicate that every property should transition.

  CodePen Embed - Learn CSS: Transitions - transition-property  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### transition-duration

The [`transition-duration`](https://developer.mozilla.org/docs/Web/CSS/transition-duration) property is used to define the length of time that a transition will take to complete.

  CodePen Embed - Learn CSS: Transitions - transition-duration  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

`transition-duration` accepts time units, either in seconds (`s`) or milliseconds (`ms`) and defaults to `0s`.

### transition-timing-function

Use the [`transition-timing-function`](https://developer.mozilla.org/docs/Web/CSS/transition-timing-function) property to vary the speed of a CSS transition over the course of the `transition-duration`.

By default, CSS will transition your elements at a constant speed (`transition-timing-function: linear`). Linear transitions can end up looking somewhat artificial, though: in real life, objects have weight and can't stop and start instantly. Easing into or out of a transition can make your transitions more lively and natural.

  CodePen Embed - Learn CSS: Transitions - transition-timing-function  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Our [module on CSS Animation](https://web.dev/learn/css/animations#animation-timing-function) has a good overview of timing functions.

You can use [DevTools](https://developer.chrome.com/docs/devtools/css/animations) to experiment with different timing functions in real-time.

![Chrome DevTools visual transition timing editor.](https://web.dev/static/learn/css/transitions/image/chrome-devtools-visual-tr-a81b123ee987d.png)

### transition-delay

Use the [`transition-delay`](https://developer.mozilla.org/docs/Web/CSS/transition-delay) property to specify the time at which a transition will start. If `transition-delay` is not specified, transitions will start instantly because the default value is `0s`. This property accepts a time unit, for example seconds (`s`) or milliseconds (`ms`).

  CodePen Embed - Learn CSS: Transitions - transition-delay  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

This property is useful for staggering transitions, achieved by setting a longer `transition-delay` for each subsequent element in a group.

  CodePen Embed - Learn CSS: Transitions - transition-delay staggered  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

`transition-delay` is also useful for debugging. Setting the delay to a negative value can start a transition further into the timeline.

### shorthand: transition

Like most CSS properties, there is a shorthand version. [`transition`](https://developer.mozilla.org/docs/Web/CSS/transition) combines `transition-property`, `transition-duration`, `transition-timing-function`, and `transition-delay`.

```
.longhand {
  transition-property: transform;
  transition-duration: 300ms;
  transition-timing-function: ease-in-out;
  transition-delay: 0s;
}

.shorthand {
  transition: transform 300ms ease-in-out 0s;
}
```

## What can and can't transition?

When writing CSS, you can specify which properties should have animated transitions. See [this MDN list of animatable CSS properties](https://developer.mozilla.org/docs/Web/CSS/CSS_animated_properties).

In general, it's only possible to transition elements that can have a "middle state" between their start and final states. For example, it's impossible to add transitions for `font-family`, because it's unclear what the "middle state" between `serif` and `monospace` should look like. On the other hand, it is possible to add transitions for `font-size` because its unit is a length that can be interpolated between.

![Diagram of shapes transitioning smoothly from one state to another, and two lines of text in different fonts that cannot be transitioned smoothly.](https://web.dev/static/learn/css/transitions/image/diagram-shapes-transitio-b51956d49a4c.jpg)

Here are some common properties you can transition.

### Transform

The [`transform`](https://developer.mozilla.org/docs/Web/CSS/transform) CSS property is commonly transitioned because it is a GPU-accelerated property that results in smoother animation that also consumes less battery. This property lets you arbitrarily scale, rotate, translate, or skew an element.

  CodePen Embed - Learn CSS: Transitions - transform  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Check out [the section on transforms](https://web.dev/learn/css/functions#transforms) in [our Functions module](https://web.dev/learn/css/functions).

### Color

Before, during, and after interaction, color can be a great indicator of state. For example, a button might change color if it's being hovered. This color change can provide feedback to the user that the button is clickable.

The `color`, `background-color`, and `border-color` properties are just a few places where color can be transitioned upon interaction.

Check out [our module on color](https://web.dev/learn/css/color).

### Shadows

Shadows are often transitioned to indicate elevation change, like from user focus.

  CodePen Embed - Learn CSS: Transitions - shadow (elevation)  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Check out [our module on shadows](https://web.dev/learn/css/shadows).

### Filters

[`filter`](https://developer.mozilla.org/docs/Web/CSS/filter) is a powerful CSS property that lets you add graphic effects on the fly. Transitioning between different `filter` states can create some pretty impressive results.

  CodePen Embed - Learn CSS: Transitions - filter  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Check out [our module on filters](https://web.dev/learn/css/filters).

## Transition triggers

Your CSS must include a change of state _and_ an event that triggers that state change for CSS transitions to activate. A typical example of such a trigger is the `:hover` [pseudo-class](https://web.dev/learn/css/pseudo-classes). This pseudo-class matches when the user hovers over an element with their cursor.

Below is a list of some pseudo-classes and events that can trigger state changes in your elements.

*   [`:hover`](https://web.dev/learn/css/pseudo-classes#hover): matches if the cursor is over the element.
*   [`:focus`](https://web.dev/learn/css/pseudo-classes#focus_focus-within_and_focus-visible): matches if the element is focused.
*   [`:focus-within`](https://web.dev/learn/css/pseudo-classes#focus_focus-within_and_focus-visible) : matches if the element or any of its descendants are focused.
*   [`:target`](https://web.dev/learn/css/pseudo-classes#target): matches when the current URL's [fragment](https://developer.mozilla.org/docs/Web/HTTP/Basics_of_HTTP/Identifying_resources_on_the_Web#fragment) matches the element's id.
*   [`:active`](https://web.dev/learn/css/pseudo-classes#active): matches when the element is being activated (typically when the mouse is pressed over it).
*   `class` change from JavaScript: when an element's CSS `class` changes via JavaScript, CSS will transition eligible properties that have changed.

## Different transitions for enter or exit

By setting different `transition` properties on hover/focus, it's possible to create some interesting effects.

```
.my-element {
  background: red;

  /* This transition is applied on the "exit" transition */
  transition: background 2000ms ease-in;
}

.my-element:hover {
  background: blue;

  /* This transition is applied on the "enter" transition */
  transition: background 150ms ease;
}
```

  CodePen Embed - Learn CSS: Transitions - diff enter/exit  

Live

Live

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Accessibility considerations

CSS transitions are not for everyone. For some people, transitions and animations can cause motion sickness or discomfort. Thankfully, CSS has a media feature called [`prefers-reduced-motion`](https://developer.mozilla.org/docs/Web/CSS/@media/prefers-reduced-motion) that detects if a user has indicated a preference for less motion from their device.

```
/*
  If the user has expressed their preference for
  reduced motion, then don't use transitions.
*/
@media (prefers-reduced-motion: reduce) {
  .my-element {
    transition: none;
  }
}

/*
  If the browser understands the media query and the user
  explicitly hasn't set a preference, then use transitions.
*/
@media (prefers-reduced-motion: no-preference) {
  .my-element {
    transition: transform 250ms ease;
  }
}
```

Check out our blog post [prefers-reduced-motion: Sometimes less movement is more](https://web.dev/articles/prefers-reduced-motion) for more information on this media feature.

## Performance considerations

When working with CSS transitions, you may encounter performance issues if you add transitions for certain CSS properties. For example, when properties such as `width` or `height` change, they push content around on the rest of the page. This forces CSS to calculate new positions for every affected element for each frame of the transition. When possible, we recommend using properties like `transform` and `opacity` instead.

Check out our [guide on high-performance CSS animations](https://web.dev/articles/animations-guide) for a deep-dive on this topic.

### Check your understanding

Test your knowledge of transitions

Which transition property is for specifying easing?

`transition-timing-function`

It's best practice to use `transition-property: all`

All properties can be transitioned.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
