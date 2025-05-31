# Autofill  |  web.dev

**Source URL:** [https://web.dev/learn/forms/autofill?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fautofill](https://web.dev/learn/forms/autofill?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fautofill)  
**Last Updated:** 2025-05-23T00:59:57.473Z  
**Extracted:** 2025-05-31 16:58:10

---

# Autofill  |  web.dev

Having to re-enter your address for the tenth time is tiring. Browsers, and you, as a developer, can help users enter data faster, and avoid re-entering data. This module teaches you how autofill works, and how `autocomplete` and other element attributes can ensure that browsers offer appropriate autofill options.

## How does autofill work?

In the [intro to autofill](https://web.dev/learn/forms/auto), you already learned the basics of autofill. But why do browsers offer autofill?

Filling out forms isn't an interesting activity, but still something you do often. Over time, you fill out many forms, and you often fill in the same data. One way to help users fill out forms faster is by offering them the option to automatically fill in form fields with previously entered data. That's autofill.

How do browsers know what data to autofill? Take a look at an example form field to find out.

```
<label for="name">Name</label>
<input name="name" id="name">
```

If you submit this form field, browsers store the value (the data you entered) along with the value of the `name` attribute (name). Some browsers also look at the `id` attribute when storing and filling in data.

Say, weeks later, you fill out another form on another website. This site also contains a form field with `name="name"`. Your browser can now offer autofill, because a value for name is already stored.

Autofill is especially useful in forms you regularly use, such as sign-up and sign-in, payment, checkout, and forms where you have to enter your name or address.

You can help browsers offer the best autofill options by using appropriate values for the `autocomplete` attribute. There are many possible values for `autocomplete`. Here is an example of addresses.

  CodePen Embed - Learn forms – autocomplete address  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Does your browser already have an address saved for you? Great! After you interact with the first field in the address form, the browser shows you a list of saved addresses. You can choose one, and the browser fills in all fields related to the address. Autofill makes filling out forms fast and easy.

Not every address form has the same fields, and the order of fields also varies. Using the correct values for `autocomplete` ensures that the browser fills in the correct values for a form. There are values for `country`, `postal-code`, and [many more](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values).

## Ensure users can sign in fast and use secure passwords

Many people aren't good at remembering passwords. The [most common password](https://en.wikipedia.org/wiki/List_of_the_most_common_passwords) is '123456', followed by other easy-to-remember combinations. How can you use secure and unique passwords without remembering them all?

Browsers have built-in passwords managers to generate, save, and fill in passwords for you. See how you can help browsers with auto-filling emails and managing passwords.

  CodePen Embed - Learn forms – autocomplete sign-up  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

You can use `autocomplete="email"` for an email field, so users get the autofill option for an email address.

As this is a sign-up form, users shouldn't get the option to fill in previously used passwords. You can use `autocomplete="new-password"` to ensure browsers offer the option to generate a new password.

On the sign-in form, you can use `autocomplete="current-password"` to tell browsers to offer the option to fill in previously saved passwords for this website.

You can set up two-factor authentication on many websites. In addition to the password, a one-time code is sent with SMS or a two-factor authentication app.

Wouldn't it be great if the code you received in the SMS message was suggested by the on-screen keyboard, and you could directly select it to fill in the value? On Safari 14 or later, you can use [`autocomplete="one-time-code"`](https://developer.apple.com/documentation/security/password_autofill/enabling_password_autofill_on_an_html_input_element) to achieve this. On Chrome on Android, you can use the [WebOTP API](https://developer.chrome.com/docs/identity/web-apis/web-otp) to achieve this with JavaScript.

Learn more about how to verify phone numbers on the web with the [SMS OTP form best practices](https://web.dev/articles/sms-otp-form).

## Help users fill in their credit card information

On many ecommerce websites, you can use your credit card to purchase products. Sites may use third-party payment platforms that provide their own forms, but if you do need to build your own payment forms, make sure people can easily fill in payment information.

You can use the `autocomplete` attribute again, to ensure browsers offer the correct autofill options.

There are values for the credit card number `cc-number`, credit card expiration date `cc-exp`, and [all other information needed](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values) for a credit card payment.

Use a single input for numbers such as credit card numbers and telephone numbers, to ensure browsers offer autofill. Use standard form elements, for example, a `<select>` for the payment card dates, instead of custom elements, to ensure autocomplete is available.

Learn more about [helping users to avoid re-entering payment data](https://web.dev/learn/forms/payment#help_users_enter_their_payment_details).

## Ensure autofill works for all your fields

In addition to addresses, account information, and credit card information, there are many more fields where browsers can help users with autofill.

When adding a telephone field to your form check if you can use any of the [available values](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values) for autocomplete. Found an appropriate value for your form field? Add it.

Using suitable values for the `autocomplete` attribute helps browsers offer the best autofill option, and helps users fill out forms faster.

## Help browsers understand that a field shouldn't be autofilled

You learned how autofill works, how you can help browsers with autofill, and why autofill makes it convenient for users to fill out forms. Sometimes, though, you don't want browsers to offer autofill.

```
<label for="one-time-code">One-time code</label>
<input autocomplete="off" type="text" name="one-time-code" id="one-time-code">
```

One place where autofill isn't helpful is when entering one-off, unique values such as a one-time code field. The value is different every time, and the browser shouldn't save values or offer an autofill option. You can use `autocomplete="off"` for such fields to prevent autofill.

Another use case for `autocomplete="off"` is a honeypot field (see [previous module](https://web.dev/learn/forms/security-privacy#a_honeypot)). Even though the field isn't visible, browsers may autofill it with the rest of the fields. Turning autofill off ensures a real user isn't identified as a bot, due to the field being completed automatically.

You should only disable autofill if you are sure it will help users.

### Check your understanding

Test your knowledge of autofill

What autocomplete value should you use for the password field in a sign-up form?

`autocomplete="new-password"`

`autocomplete="current-password"`

## Resources

*   The [autocomplete attribute](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete).
    *   [Payment and address form best practices](https://web.dev/articles/payment-and-address-form-best-practices)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
