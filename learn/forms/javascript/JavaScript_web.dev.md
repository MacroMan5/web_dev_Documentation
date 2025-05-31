# JavaScript  |  web.dev

**Source URL:** [https://web.dev/learn/forms/javascript?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fjavascript](https://web.dev/learn/forms/javascript?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fjavascript)  
**Last Updated:** 2025-05-23T01:00:48.752Z  
**Extracted:** 2025-05-31 16:58:10

---

# JavaScript  |  web.dev

JavaScript

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

## Respond to form events

You can use JavaScript to respond to user interactions on your form, reveal additional form fields, submit a form, and much more.

### Help users fill in additional form controls

Imagine that you built a survey form. After a user selects one option, you want to show an additional `<input>` to ask a specific question related to the selection. How can you only show the relevant `<input>` element?

  CodePen Embed - Learn forms – additional form field  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

You can use JavaScript to reveal an `<input>` only when the associated `<input type="radio">` is currently selected.

```
if (event.target.checked) {
    // show additional field
} else {
   // hide additional field
}
```

Let's look at the [JavaScript code](https://codepen.io/web-dot-dev/pen/8e1e7a38790c75c267a978efa1d8e937?editors=0010) for the demo. Have you noticed the `aria-controls`, and `aria-expanded` attributes? Use these [ARIA attributes](https://developer.mozilla.org/docs/Web/Accessibility/ARIA) to help screen reader users understand when an additional form control is shown or hidden.

### Ensure users can submit a form without leaving a page

Imagine you have a comment form. When a reader adds a comment and submits the form, it would be ideal if they could immediately see the comment without a page refresh.

To achieve this, listen to the `onsubmit` event, then use `event.preventDefault()` to prevent the default behavior, and send the `FormData` using the [Fetch API](https://developer.mozilla.org/docs/Web/API/Fetch_API).

  CodePen Embed - Learn forms – FormData  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Your backend script can check if a `POST` request appears to be from the browser (using the `action` attribute of a form element, where `method="post"`) or from JavaScript, such as a `fetch()` request.

```
if (req.xhr || req.headers.accept.indexOf('json') !== -1) {
    // return JSON
} else {
    // return HTML
}
```

Always notify screen reader users about dynamic content changes. Add an element with the `aria-live="polite"` attribute to your HTML, and update the content of the element after a change. For example, update the text to 'Your comment was successfully posted', after a user submits a comment.

Learn more about [ARIA live regions](https://developer.mozilla.org/docs/Web/Accessibility/ARIA/ARIA_Live_Regions).

## Validation with JavaScript

### Ensure error messages align with your site style and tone

The wording of default error messages differs between browsers. How can you make sure the same message is shown to all users, and that the message aligns with your site's [style and tone](https://developers.google.com/style/tone)? Use the [`setCustomValidity()`](https://developer.mozilla.org/docs/Web/API/HTMLInputElement/setCustomValidity) method of the [Constraint Validation API](https://developer.mozilla.org/docs/Web/API/Constraint_validation) to define your own error messages.

  CodePen Embed - Learn forms – validationMessage  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Ensure users are notified about errors in real time

The built-in HTML features for form validation are great for notifying users about invalid form fields before the data is sent to your backend. Wouldn't it be great to notify users as soon as they leave a form field?

  CodePen Embed - Learn forms – real-time validation  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Listen for the [`blur`](https://developer.mozilla.org/docs/Web/API/Element/blur_event) event which fires when an element loses focus, and use the [`ValidityState`](https://developer.mozilla.org/docs/Web/API/ValidityState) interface to detect if a form control is invalid.

### Ensure users can see the password they entered

The text entered for `<input type="password">` is obscured by default, to respect the privacy of users. Help users to enter their password, by showing a `<button>` to toggle the visibility of the entered text.

  CodePen Embed - Learn forms – reveal password  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

[Try out the demo](https://codepen.io/web-dot-dev/pen/bd8577c5380c436dba2788c7a2c8652a). Toggle the visibility of the entered text, by using the **Show Password** `<button>`. How does this work? Clicking on **Show Password**, changes the `type` attribute of the password field from `type="password"` to `type="text"`, and the `<button>` text changes to 'Hide Password'.

It's important to make the **Show Password** button accessible. Connect the `<button>` with the `<input type="password">` using the `aria-controls` attribute.

To notify screen reader users if the password is currently shown or hidden, use a hidden element with `aria-live="polite"`, and change its text accordingly. It's important to enable screen reader users to know when a password is displayed and visible to someone else looking at their screen.

```
<span class="visually-hidden" aria-live="polite">
    <!-- Dynamically change this text with JavaScript -->
</span>
```

Learn more about [implementing a show password option](https://technology.blog.gov.uk/2021/04/19/simple-things-are-complicated-making-a-show-password-option/).

## Resources

*   [FormData](https://developer.mozilla.org/docs/Web/API/FormData)
*   [Constraint Validation API](https://developer.mozilla.org/docs/Web/API/Constraint_validation)
*   [`<input type="password">`](https://developer.mozilla.org/docs/Web/HTML/Element/input/password)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
