# Use forms to get data from users  |  web.dev

**Source URL:** [https://web.dev/learn/forms/form-element?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fform-element](https://web.dev/learn/forms/form-element?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fform-element)  
**Last Updated:** 2025-05-23T00:59:00.383Z  
**Extracted:** 2025-05-31 16:58:10

---

# Glitch

Use forms to get data from users

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

Learn the basics of using a form on the web with this introduction to the form element.

Imagine you want to ask people on your website about their favorite animal. As a first step, you need a way to collect the data.

How do you do this with HTML?

In HTML, you can build this using the form element (`<form>`), an `<input>` with a `<label>`, and a submit `<button>`.

## What is a form element?

```
<form>
  <label for="animal">What is your favorite animal?</label>
  <input type="text" id="animal" name="animal">
  <button>Save</button>
</form>
```

The form element consists of the start tag `<form>`, optional attributes defined in the start tag, and an end tag `</form>`.

Between the start and end tag, you can include form elements like `<input>` and `<textarea>` for different types of user input. You will learn more about [form elements](https://web.dev/learn/forms/form-fields) in the next module.

## Where is the data processed?

When a form is submitted (for example, when the user clicks the **Submit** button), the browser makes a request. A script can respond to that request and process the data.

By default, the request is made to the page where the form is shown.

Say you want a script running at `https://web.dev` to process the form data—how would you do that? [Try it out](https://codepen.io/web-dot-dev/pen/fbf90faccc7a22e208c2a507f33be598?editors=1100)!

You can select the location of the script by using the `action` attribute.

<form action="https://example.com/animals">
...
</form>

The preceding example makes a request to `https://example.com/animals`. A script on the `example.com` backend can handle requests to `/animals` and process data from the form.

## How is the data transferred?

By default, form data is sent as a `GET` request, with the submitted data appended to the URL. If a user submits 'frog' in the example above, the browser makes a request to the following URL:

```
https://example.com/animals?animal=frog
```

In this case, you can access the data on the frontend or the backend by getting the data from the URL.

If you want, you can instruct the form to use a `POST` request by changing the method attribute.

```
<form method="post">
...
</form>
```

Using `POST`, the data is included in the [body of the request](https://developer.mozilla.org/docs/Web/HTTP/Methods/POST#example).

The data will not be visible in the URL and can only be accessed from a frontend or backend script.

### What method should you use?

There are use cases for both methods.

For forms that process sensitive data use the `POST` method. The data is encrypted (if you use HTTPS) and only accessible by the backend script that processes the request. The data is not visible in the URL. A common example is a sign-in form.

If the data is shareable, you can use the `GET` method. This way the data will be added to your browser history as it is included in the URL. Search forms often use this. This way you can bookmark a search result page.

Now that you've learned about the form element itself, it's time to learn about [form fields](https://web.dev/learn/forms/form-fields) to make your forms interactive.

### Check your understanding

Test your knowledge of the form element

What does the start tag of the form element look like?

What attribute can you use to define where the `<form>` is processed?

What is the default request method?

## Resources

[The `<form>` element](https://developer.mozilla.org/docs/Web/HTML/Element/form).

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
