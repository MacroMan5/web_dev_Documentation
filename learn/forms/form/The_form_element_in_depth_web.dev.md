# The form element in depth  |  web.dev

**Source URL:** [https://web.dev/learn/forms/form?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fform](https://web.dev/learn/forms/form?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fform)  
**Last Updated:** 2025-05-23T01:00:13.950Z  
**Extracted:** 2025-05-31 16:58:10

---

# The form element in depth | web.dev

In a previous module, you learned [how to use the `<form>` element](https://web.dev/learn/forms/form-element). In this module, you learn how a form works, and when to use a form.

## Should you use a `<form>` element?

You don't always need to put form controls in a `<form>` element. For example, you might provide a `<select>` element for users to choose a product category. You don't need a `<form>` element here, as you're not storing or processing data on your backend.

However, in most cases when you store or process data from users, you should use the `<form>` element. As you will learn in this module, using a `<form>` gives you a lot of built-in functionality from browsers that you would otherwise have to build yourself. A `<form>` also has many accessibility features built-in by default. If you want to avoid a page reload when a user submits a form, you can still use the `<form>` element, but enhance it with [JavaScript](https://web.dev/learn/forms/javascript#ensure_users_can_submit_a_form_without_leaving_a_page).

## How does a `<form>` work?

You learned that a `<form>` is the best way to handle user data. You may wonder now, how does a form work?

The `<form>` is a container for interactive form controls.

```
<form method="post">
  <label for="name">Name</label>
  <input type="text" name="name" id="name">
  <button formaction="/name">Save</button>
</form>
```

## How does form submission work?

When you submit a `<form>`, the browser checks the `<form>` attributes. The data is sent as a `GET` or `POST` request according to the `method` attribute. If no `method` attribute is present, a `GET` request is made to the URL of the current page.

How can you access and process the form data? The submitted data can be handled by JavaScript on the frontend using a `GET` request, or by code on the backend using a `GET` or `POST` request. Learn more about [request types and transferring form data](https://web.dev/learn/forms/form-element#where_is_the_data_processed).

When the form is submitted, the browser makes a request to the URL that is the value of the `action` attribute. In addition, the browser checks if the **Submit** button has a `formaction` attribute. If this is the case, the URL defined there is used.

Furthermore, the browser looks up additional attributes on the `<form>` element, for example, to decide if the form should be validated (`novalidate`), autocomplete should be used (`autocomplete="off"`) or what encoding should be used (`accept-charset`).

[Try to build a form](https://codepen.io/web-dot-dev/pen/c7d89671f738240187a86cda1074d554) where users can submit their favorite color. The data should be sent as a `POST` request, and the URL where the data will be processed should be `/color`.

One possible solution is using this form:

<form method="post" action="/color">
    <label for="color">What is your favorite color?</label>
    <input type="text" name="color" id="color">
    <button>Save</button>
</form>

## Ensure users can submit your form

There are two ways to submit a form. You can click the **Submit** button, or press `Enter` while using any form control.

You can add a **Submit** button in various ways. One option is to use a `<button>` element inside your form. As long as you don't use `type="button"` it works as a **Submit** button. Another option is to use `<input type="submit" value="Submit">`.

A third option is to use `<input type="image" alt="Submit" src="submit.png">`, to create a graphical **Submit** button. However, now that you can create graphical buttons with CSS, it's not recommended to use `type="image"`.

## Enable users to submit files

Use `<input type="file">` to enable people to upload and submit files if necessary.

```
<label for="file">Choose file to upload</label>
<input type="file" id="file" name="file" multiple>
```

First, add an `<input>` element with `type="file"` to your form. Add the `multiple` attribute if users should be able to upload multiple files.

  CodePen Embed - Learn forms – file upload  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

One more change is needed to ensure users can upload files—set the `enctype` attribute on your form. The default value is `application/x-www-form-urlencoded`.

```
<form method="post" enctype="multipart/form-data">
…
</form>
```

To make sure files can be submitted, change it to `multipart/form-data`. Without this encoding, files can't be sent with a `POST` request.

### Check your understanding

Test your knowledge of the form element

What value for `enctype` is needed to submit files?

Is it possible to send user data without a `<form>`

How can you submit a `<form>`?

Click on an `<input type="image">`.

## Resources

*   [The form HTML element](https://developer.mozilla.org/docs/Web/HTML/Element/form)
*   [Submit button best practices](https://web.dev/articles/payment-and-address-form-best-practices#html-button)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
