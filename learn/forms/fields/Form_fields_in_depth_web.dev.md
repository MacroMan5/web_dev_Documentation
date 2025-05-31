# Form fields in depth  |  web.dev

**Source URL:** [https://web.dev/learn/forms/fields?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Ffields](https://web.dev/learn/forms/fields?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Ffields)  
**Last Updated:** 2025-05-23T01:00:22.747Z  
**Extracted:** 2025-05-31 16:58:10

---

# Form fields in depth | web.dev

Form fields in depth

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

## What form fields can I use?

To provide the best possible user experience, make sure to use the element and element `type` that's most appropriate for the data the user is entering.

### Help users fill in text

To provide users with a form field for inserting text, use the `<input>` element. It's the best choice for single words and short texts. For longer text, use the `<textarea>` element. This allows multiple lines of text, and makes it easier for the user to see the text they entered, as the element is scrollable and resizable.

### Ensure users enter data in the correct format

Do you want to help users fill in a telephone number? Change the `type` attribute to `type="tel"` for the `<input>`. Users on mobile devices get an adapted on-screen keyboard, ensuring they can enter the telephone number faster and more easily.

For an email address, use `type="email"`. Again, an adapted on-screen keyboard is shown. Use the `required` attribute to make the form field mandatory. When the form is submitted, the browser checks that the input has a value and that it's valid: in this case, that it's a well-formatted email address.

Learn more about the different [input types](https://developer.mozilla.org/docs/Web/HTML/Element/input#input_types). These also provide built-in [validation features](https://web.dev/learn/forms/validation).

### Help users fill in dates

When do you want to start your next trip? To help users fill in dates, use `type="date"`. Some browsers show the format as a placeholder such as `yyyy-mm-dd`, demonstrating how to enter the date.

All modern browsers provide custom interfaces for selecting dates in the form of a date picker.

  CodePen Embed - Learn forms – input type="date"  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

### Help users select an option

To ensure users can select or unselect one possible option, use `type="checkbox"`. Do you want to offer multiple options? Depending on your use case, there are various alternatives. First, let's look at possible solutions if users should only be able to choose a single option.

You can use multiple `<input>` elements with `type="radio"` and the same `name` value. Users see all options at once, but can only choose one.

  CodePen Embed - Learn forms – input type="radio"  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Another option is to use the `<select>` element. Users can scroll through a list of available options and choose one.

  CodePen Embed - Learn forms – select element  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

For some use cases, such as choosing a range of numbers, `<input>` of type `range` may be a good option.

  CodePen Embed - Learn forms – input type="range"  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Do you need to offer the ability to select multiple options? Use a `<select>` element with the `multiple` attribute or multiple `<input>` elements of type `checkbox`.

You may also use an `<input>` in combination with the [`<datalist>`](https://developer.mozilla.org/docs/Web/HTML/Element/datalist) element. This gives you a combination of a text field and a list of `<option>` elements.

### Ensure users can fill in different types of data

There are more input types for specific use cases.

There is an `<input>` of type `color` to provide users with a color picker in supported browsers, and there are various other types as well. To ensure users can enter their password, use `<input>` with `type="password"`. Every character entered is obscured by an asterisk ("\*") or a dot ("•"), to ensure the password can't be read.

Do you want to include a unique security token in the form data? Use `<input>` with `type="hidden"`. The value of an `<input>` of type `hidden` can't be seen or modified by users.

To enable users to upload and submit files, use `<input>` with `type="file"`.

  CodePen Embed - Learn forms – input type="file"  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

You can also define [custom elements](https://web.dev/articles/more-capable-form-controls#form-associated_custom_elements) if you have a special use case, where no built-in element or type is suitable.

## Help users fill out your form

There are many form elements and types, but which one should you choose?

For some use cases, it's straightforward to choose the appropriate element and type, such as `<input type="date">`. For others, it depends. For example, you can use multiple `<input>` elements with `type="checkbox"` or a `<select>` element. Learn more about [choosing between listboxes and dropdown lists](https://www.nngroup.com/articles/listbox-dropdown/).

In general, make sure to [test your form with real users](https://web.dev/learn/forms/usability-testing) to find the best form element and type.

### Check your understanding

Test your knowledge of form fields

Is it possible to upload multiple files with a form control?

Yes, using `<input type="files">`.

Yes, using `<input type="file" multiple>`.

Yes, using `<input type="multiple-files">`.

What's the difference between `type="text"` and `type="password"`?

A custom interface for entering passwords is shown for `type="password"`.

An adapted on-screen keyboard for entering passwords is shown for `type="password"`.

When using `type="password"` every character entered is obscured by an asterisk (`*`) or a dot (`•`).

## Resources

*   [The `<input>` element](https://developer.mozilla.org/docs/Web/HTML/Element/Input)
*   [The `<textarea>` element](https://developer.mozilla.org/docs/Web/HTML/Element/textarea)
*   [The `<select>` element](https://developer.mozilla.org/docs/Web/HTML/Element/select)
*   [`<input>` types](https://developer.mozilla.org/docs/Web/HTML/Element/input#input_types)
*   [Custom form elements](https://web.dev/articles/more-capable-form-controls#form-associated_custom_elements)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
