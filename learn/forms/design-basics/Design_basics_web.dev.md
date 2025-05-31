# Design basics  |  web.dev

**Source URL:** [https://web.dev/learn/forms/design-basics?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fdesign-basics](https://web.dev/learn/forms/design-basics?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fdesign-basics)  
**Last Updated:** 2025-05-23T00:59:28.046Z  
**Extracted:** 2025-05-31 16:58:10

---

# Design basics  |  web.dev

In the first section, you learned how to build a basic form. This section is all about best practices. In this module, learn about user experience (UX), and why a well-implemented user interface (UI) can make a big difference.

## Creating user-friendly interfaces

Filling out forms can be time-consuming and frustrating. It doesn't have to be. To guarantee a great UX, make sure the UI is intuitive. Ensure you deliver optimal form structure and graphic design (layout, spacing, font size and color), and logical UI (such as label wording and appropriate input types). Let's have a look at how you can improve your form and make it easy to use.

## Labels

Do you remember what the `<label>` element is for? A label describes a form control. A visible and well-written label helps the user understand the purpose of a form control.

### Use a label for every form control

Do you want to add a new form control to your form? Start by adding the label for the new field. This way, you don't forget to add it.

Adding labels first also helps you to focus on the form's goals–what data do I need here? Once this is clear, you can focus on helping the user enter data and complete the form.

### Label wording

Say that you want to describe an email field. You could do so as follows:

```
<label for="email">Enter your email address</label>
```

Or you could describe it like this:

```
<label for="email">Email address</label>
```

Which description do you choose?

For our example, the wording 'Email address' is preferred, since short labels are easier to scan, reduce visual clutter, and help users to understand what data is needed faster.

## Label position

With [CSS](https://web.dev/learn/css), you can position a label on the top, bottom, left, and right of a form control. Where do you place it?

[Research shows](https://ai.googleblog.com/2014/07/simple-is-better-making-your-web-forms.html) that best practice is to [position the label above the form control](https://www.uxmatters.com/mt/archives/2006/07/label-placement-in-forms.php), so the user can scan a form quickly and see which label belongs to which form control.

## Designing forms

Good form design can [significantly reduce form abandonment rates](https://baymard.com/blog/checkout-flow-average-form-fields). Help users enter data by using the appropriate element and input type There are various [form elements and input types](https://web.dev/learn/forms/fields) you can choose from. To offer the best UX, use the most suitable element and input type for your use case. If the user should fill in multiple lines of text, use the `<textarea>` element. Where they need to accept your site's terms and conditions, use `<input type="checkbox">`.

You should also visually differentiate between different types of form controls. A button should look like a button. An input like an input. Make it easy for users to recognize the purpose of a form control. For example, If something looks like a link, clicking on it should open a new page, and not submit a form.

  CodePen Embed - Learn forms – button styles as link  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Help users navigate forms

An extravagant layout can be fun, but may get in the way of completing a form.

In particular, [research shows](https://baymard.com/blog/avoid-multi-column-forms) that it's best to use only a single column. Users don't want to spend time searching where the next form control is. By using one column, there is only one direction to follow.

### Help users interact with forms

To avoid accidental taps and clicks, and help users interact with your form, make your buttons big enough. The recommended [tap target size](https://web.dev/articles/accessible-tap-targets) of a button is at least 48px. You should also add enough spacing between form controls using the `margin` CSS property to help avoid accidental interactions.

The default size of form controls is too small to be really usable. You should increase the size by using `padding` and changing the default `font-size`.

You can define different sizes for different pointing devices, for example, a mouse, using the `pointer` CSS media feature.

```
// pointer device, for example, a mouse
@media (pointer: fine) {
  input[type="checkbox"] {
    width: 15px;
    height: 15px;
  }
}

// pointer device of limited accuracy, for example, a touch-based device
@media (pointer: coarse) {
  input[type="checkbox"] {
    width: 30px;
    height: 30px;
  }
}
```

Learn more about the [`pointer` CSS media feature](https://developer.mozilla.org/docs/Web/CSS/@media/pointer).

### Show errors where they happen

To make it straightforward for users to find out which form control needs their attention, display error messages next to the form control they refer to. When displaying errors on form submission, make sure to navigate to the first invalid form control.

### Make it clear to users what data to enter

Make sure users understand how to enter valid data. Do they need to enter at least eight characters for a password? Tell them.

```
<label for="password">Password (required)</label>
<input required minlength="8" type="password" id="password" name="password" aria-describedby="password-minlength">
<span id="password-minlength">Enter at least eight characters</span>
```

### Make it clear to users which fields are required

```
<label for="name">Name (required)</label>
<input name="name" id="name" required>
```

If a field is mandatory, make it obvious! [The Anatomy of Accessible Forms](https://www.deque.com/blog/anatomy-of-accessible-forms-required-form-fields/) explains alternatives for indicating required fields. If most fields in a form are required, it may be better to [indicate optional fields](https://www.lukew.com/ff/entry.asp?725).

How can you connect error messages to form controls to make them accessible for screen readers? You can learn about this in [the next module](https://web.dev/learn/forms/accessibility).

### Check your understanding

Test your knowledge of designing forms

How do you describe a form control?

Using the `description` attribute.

Using the `<label>` element.

Using the `placeholder` attribute.

Using the `<description>` element.

What's the recommended tap target size?

Big enough to tap it with a potato.

Where should you place error messages?

At the top of the `<form>`.

Never show error messages.

## Resources

*   [Create Amazing Forms](https://web.dev/learn/forms)
*   [Best Practices For Mobile Form Design](https://www.smashingmagazine.com/2018/08/best-practices-for-mobile-form-design/)
*   [Baymard Institute: E-Commerce UX Research](https://baymard.com/blog)
*   [Don't Make Me Think](https://en.wikipedia.org/wiki/Don%27t_Make_Me_Think)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
