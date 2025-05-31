# Accessibility  |  web.dev

**Source URL:** [https://web.dev/learn/forms/accessibility?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Faccessibility](https://web.dev/learn/forms/accessibility?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Faccessibility)  
**Last Updated:** 2025-05-23T00:59:39.337Z  
**Extracted:** 2025-05-31 16:58:10

---

# Accessibility  |  web.dev

The form you build is for people. People use different devices. Some use a mouse, some a touch device, some the keyboard, some a device controlled by eye movements. Some use a screen reader, some a small screen, some use text enlargement software. Everybody wants to use your form. Learn how to make your form accessible and usable for everyone.

## Ensure users understand the purpose of a form field

There are many [form controls](https://web.dev/learn/forms/fields) you can choose from. What do they all have in common? Every form control must have an associated `<label>` element. The `<label>` element describes the purpose of a form control. The `<label>` text is visually associated with the form control, and read out by screen readers.

In addition, tapping or clicking the `<label>` focuses the associated form control, making it a larger target.

## Use meaningful HTML to access built-in browser features

In theory, you could build a form using only `<div>` elements. You can even make it look like a native `<form>`. What's the problem with using [non-semantic](https://developer.mozilla.org/docs/Glossary/Semantics) elements?

Built-in form elements provide a lot of built-in features. Let's have a look at an example.

  CodePen Embed - Learn forms – accessible and inaccessible input  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Visually, the `<input>` (the first one in the example) and the `<div>` look the same. You can even insert text for both, as the `<div>` has a [`contenteditable`](https://developer.mozilla.org/docs/Web/HTML/Global_attributes/contenteditable) attribute. There are lots of differences, though, between using an appropriate `<input>` element and a `<div>` looking like an `<input>`.

A screen reader user doesn't recognize the `<div>` as an input element, and isn't able to complete the form. All the screen reader user hears is 'Name', with no indication that the element is a form control for adding text.

Clicking on `<div>Name</div>` doesn't focus the `<div>` that goes with it, whereas the `<label>` and the `<input>` are connected by using the `for` and `id` attributes.

After submitting the form, the data entered in the `<div>` isn't included in the request. While attaching the data with JavaScript is possible, an `<input>` does that by default.

Built-in form elements have other features. For example, with appropriate form elements and the correct `inputmode` or `type`, an on-screen keyboard shows appropriate characters. Using the `inputmode` attribute on a `<div>` cannot do that.

## Ensure users are aware of the expected data format

You can define various validation rules for a form control. For example, say a form field should always have at least eight characters. You use the `minlength` attribute, indicating the validation rule to browsers. How can you ensure users also know about the validation rule? Tell them.

  CodePen Embed - Learn forms – validation rule  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Add information about the expected format directly beneath the form control. To make it clear for assistive devices, use the `aria-describedby` attribute on the form control, and an `id` on the error message with the same value, to connect both.

## Help users find the error message for a form control

In a previous module about [validation](https://web.dev/learn/forms/validation), you learned how to show error messages in case of invalid data entry.

```
<label for="name">Name</label>
<input type="text" name="name" id="name" required>
```

For example, if a field has a `required` attribute, and invalid data is entered, the browser shows an error message next to the form control when the form is submitted. Screen readers also announce the error message.

You can also define your own error message:

  CodePen Embed - Learn forms – real-time validation  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

This example needs more changes to connect the error message to the form control.

A simple approach is to use the `aria-describedby` attribute on the form control that matches the `id` on the error message element. Then, use [`aria-live="assertive"`](https://developer.mozilla.org/docs/Web/Accessibility/ARIA/ARIA_Live_Regions) for the error message. ARIA live regions announce an error to screen reader users the moment the error is shown.

The problem with this approach for forms with multiple fields, is that `aria-live` will usually only announce the first error in the case of multiple errors. As explained in [this article about multiple `aria-live` announcements on the same action](https://gaurav5430.medium.com/quick-accessibility-wins-multiple-aria-live-on-single-action-caveat-b79a6f41e7cc) you could create a single message by concatenating all the errors. Another approach would be to announce that there are errors, then announce individual errors when the field is focused.

## Ensure users recognize errors

Sometimes designers color the invalid state red, using the `:invalid` pseudo-class. However, to communicate an error or success, you should never rely only on color. For people with red-green color blindness, a green and a red border look almost the same. It's impossible to see if the message is related to an error.

In addition to color, use an icon, or prefix your error messages with the error type.

```
<span class="error">
  <strong>Error:</strong>Please use at least eight characters.
</span>
```

## Help users to navigate your form

You can change the visual order of form controls with CSS. A disconnect between visual order and keyboard navigation (DOM order) is problematic for screen reader and keyboard users.

Learn more about how to ensure [visual order on the page follows DOM order](https://web.dev/visual-order-follows-dom).

## Help users to identify the currently focused form control

Use your keyboard to navigate through [this form](https://codepen.io/web-dot-dev/pen/c4ab903b77cdfc05dac4707fca69b997). Did you recognize that the styling of the form controls changed once they were active? This is the default focus style. You can override it with the [`:focus`](https://developer.mozilla.org/docs/Web/CSS/:focus) CSS pseudo-class. Whatever styles you use inside `:focus`, always make sure the visual difference between the default state and the focus state is recognizable.

Learn more about [designing focus indicators](https://www.sarasoueidan.com/blog/focus-indicators/).

## Ensure your form is usable

You can identify many common issues by filling out your form with different devices. Use only your keyboard, use a screen reader (such as [NVDA](https://www.nvaccess.org/) on Windows or [VoiceOver](https://en.wikipedia.org/wiki/VoiceOver) on Mac), or zoom the page to 200%. Always test your forms on different platforms, especially devices or settings you don't use every day. Do you know someone using a screen reader, or someone using text enlargement software? Ask them to fill out your form. Accessibility reviews are great, testing with real users is even better.

Learn more about doing an [accessibility review](https://web.dev/articles/how-to-review) and how to [test with real users](https://web.dev/learn/forms/usability-testing).

## Resources

*   [WebAIM: Creating Accessible Forms](https://webaim.org/techniques/forms)
*   [WCAG: autocomplete accessibility benefits](https://www.w3.org/WAI/WCAG21/Understanding/identify-input-purpose.html)
*   [Focus Indicators](https://www.sarasoueidan.com/blog/focus-indicators/)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
