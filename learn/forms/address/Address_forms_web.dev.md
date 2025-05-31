# Address forms  |  web.dev

**Source URL:** [https://web.dev/learn/forms/address?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Faddress](https://web.dev/learn/forms/address?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Faddress)  
**Last Updated:** 2025-05-23T01:01:04.967Z  
**Extracted:** 2025-05-31 16:58:10

---

# Address forms  |  web.dev

Address forms

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

Filling in an address can be time-consuming and frustrating. What is an **Address line 2**? You may not have a surname, so what should you enter in a **Surname** field? Avoid these confusions and help users fill out address forms.

  CodePen Embed - Learn forms – address form  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

## Ensure your address form is easy to use

Many forms use one field for first name and one for surname. However, some people don't have a surname, or their names don't have two parts, so how should they fill in the surname field? Use a single `<input>` for the name field. Learn more about [handling different name formats](https://web.dev/learn/forms/internationalization#ensure_your_form_can_handle_different_name_formats).

Also use a single `<input>` for the street address–not every address has a street number.

Be careful with form control descriptions. For example, users in the US say **ZIP**, in the UK **postcode**. Use `<label for="zip">ZIP or postal code (optional)</label>` to make sure users know what data to enter. Make the postal code field optional–not every address has a postal code.

## Help users enter their address

The `autocomplete` attribute can help users re-enter their address:

*   `autocomplete="name"`
*   `autocomplete="street-address"`
*   `autocomplete="postal-code"`
*   `autocomplete="country"`

You can define multiple values separated by a space for `autocomplete`. Say you have a form with a shipping address and another form for a billing address. To tell the browser which postal code is for the billing address, you can use `autocomplete="billing postal-code"`. For the shipping address, use `shipping` as the first value.

Change the label for the `Enter` key on on-screen keyboards with the `enterkeyhint` attribute. Use `enterkeyhint="done"` for the last form control, and `enterkeyhint="next"` for the other form controls.

## Resources

*   [Payment and address forms best practices](https://web.dev/articles/payment-and-address-form-best-practices)
*   [Form Usability: Getting ‘Address Line 2' Right](https://baymard.com/blog/address-line-2)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
