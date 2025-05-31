# Help users avoid re-entering data in forms  |  web.dev

**Source URL:** [https://web.dev/learn/forms/auto?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fauto](https://web.dev/learn/forms/auto?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fauto)  
**Last Updated:** 2025-05-23T00:59:20.556Z  
**Extracted:** 2025-05-31 16:58:10

---

# Help users avoid re-entering data in forms | web.dev

Help users avoid re-entering data in forms

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

After learning about the [form element](https://web.dev/learn/forms/form-element) and how to make a form [interactive](https://web.dev/learn/forms/form-fields), let's see how you can help users avoid re-entering data.

## Make the most of autofill

Filling out forms can be time-consuming. For example, re-entering your address repeatedly on every site where you want to buy something is not a great shopping experience.

Autofill can help you here. You enter your address once. From now on, your browser will offer you the option to fill in the same address for other forms automatically.

You moved to another city? Don't worry about getting the old address as an option forever. You can edit the address data your browser has saved for you to keep it up-to-date.

## How does autofill work in the browser?

An address field can look very different on different sites. How does a browser know that it is an address field?

Browsers use heuristics to identify an address field. What are the values of the `name`, `type`, and `id` attributes? Is there an [`autocomplete` attribute](https://web.dev/learn/forms/auto#autocomplete) present on the form control?

Based on this information, browsers can offer the option to autofill a field with previously entered data of the same type. Browsers can even offer to autofill an entire form.

## Help browsers with autofill

Let's see what you can do to help browsers offer the correct autofill options.

### Use sensible attribute values

As you learned, browsers can identify the data type by looking at the attributes of a form control.

```
<label for="email">Email</label>
<input type="email" name="email" id="email">
```

Do you have a field where users should enter their email address? Use `email` as a value for the `name`, `id`, and `type` attribute. Three hints for the browser that this is an email field.

### The autocomplete attribute

There are other examples where it can still be hard for browsers to identify the data type solely from the `name`, `id`, and `type` attributes. You can help here by using the `autocomplete` attribute.

  CodePen Embed - Learn forms – autocomplete  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Have you entered a name before in the browser you're using? The browser will probably offer you the option to fill it in again for this field in the demo.

You can learn more about using [autocomplete and autofill](https://web.dev/learn/forms/autofill) in a later module.

### Check your understanding

Test your knowledge of autofill

Based on which attributes is autofill offered?

The `autocomplete` attribute

## Resources

*   [The autocomplete attribute](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete)
*   [Autofill: What web devs should know, but don't](https://cloudfour.com/thinks/autofill-what-web-devs-should-know-but-dont)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
