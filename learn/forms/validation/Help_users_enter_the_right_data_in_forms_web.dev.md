# Help users enter the right data in forms  |  web.dev

**Source URL:** [https://web.dev/learn/forms/validation?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fvalidation](https://web.dev/learn/forms/validation?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fvalidation)  
**Last Updated:** 2025-05-23T00:59:23.244Z  
**Extracted:** 2025-05-31 16:58:10

---

# Help users enter the right data in forms | web.dev

Browsers have built-in features for validation to check that users have entered data in the correct format. You can activate these features by using the correct elements and attributes. On top of that, you can enhance form validation with CSS and JavaScript.

## Why should you validate your forms?

You learned in the previous module how to help users avoid having to repeatedly [re-enter information](https://web.dev/learn/forms/auto) in forms. How can you help users enter data that's valid?

It's frustrating to fill out a form without knowing which fields are required, or the constraints of those fields. For example, you enter a username and submit a form—only to find out that usernames must have at least eight characters.

You can help users with that by defining validation rules and communicating them.

## Help users from accidentally missing required fields

You can use HTML to specify the correct format and constraints for data entered in your forms. You also need to specify which fields are mandatory.

  CodePen Embed - Learn forms – required  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Try to submit this form without entering any data. Do you see an error message attached to the `<input>` telling you that the field is required?

This happens because of the `required` attribute.

```
<label for="name">Name (required)</label>
<input required type="text" id="name" name="name">
```

You already learned that you can use many more types, for example, `type="email"`. Let's have a look at a required email `<input>`.

  CodePen Embed - Learn forms – required type email  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Try to submit this form without entering any data. Is there any difference from the demo before? Now insert your name in the email field and try to submit. You see a different error message. How is that possible? You get a different message because the value you entered isn't a valid email address.

The `required` attribute tells the browser that the field is mandatory. The browser also tests if the entered data matches the format of the `type`. The email field shown in the example is only valid if it's not empty and if the entered data is a valid email address.

## Help the user enter the correct format

You learned how to make a field mandatory. How would you instruct the browser that a user must enter at least eight characters for a form field?

  CodePen Embed - Learn forms – minlength password  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Give the demo a try. After your change, you should not be able to submit the form if you enter less than eight characters.

<label for="password">Password (required)</label>
<input required="" minlength="8" type="password" id="password" name="password">

The name of the attribute is `minlength`. Set the value to `8` and you have the desired validation rule. If you want the opposite, use `maxlength`.

## Communicate your validation rules

```
<label for="password">Password (required)</label>
<input required minlength="8" type="password" id="password"
  name="password" aria-describedby="password-minlength">
<div id="password-minlength">Enter at least eight characters</div>
```

Make sure all users understand your validation rules. For this, connect the form control with an element that explains the rules. To do so, add an `aria-describedby` attribute to the element with the `id` of the form.

## Pattern attribute

Sometimes you want to define more advanced validation rules. Again, you can use an HTML attribute. It's called `pattern`, and you can define a [regular expression](https://regex101.com/) as the value.

```
<label for="animal">What is your favorite animal? (required)</label>
<input required pattern="[a-z]{2,20}" type="text" id="animal" name="animal">
```

Here, only lowercase letters are allowed; the user has to enter at least two characters, and not more than twenty.

How would you change the `pattern` to also allow uppercase letters? [Try it out](https://codepen.io/web-dot-dev/pen/bc12240b7cb5b52076621d73a8a29cf6).

The correct answer is `pattern="[a-zA-Z]{2,20}"`.

## Add styles

You have now learned how to add validation in HTML. Wouldn't it be great if you could also style form controls based on the validation status? This is possible with CSS.

## How to style a required form field

Show the user that a field is mandatory before they interact with your form.

  CodePen Embed - Learn forms – :required  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

You can style `required` fields with the `:required` CSS pseudo class.

```
input:required {
  border: 2px solid;
}
```

## Style invalid form controls

Do you remember what happens if data entered by the user is invalid? The error message attached to the form control appears. Wouldn't it be great to adapt the appearance of the element when this happens?

  CodePen Embed - Learn forms – :invalid  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

You can use the `:invalid` [pseudo-class](https://web.dev/learn/css/pseudo-classes) to add styles to invalid form controls. In addition, there is also the `:valid` pseudo-class for styling valid form elements.

There are more ways to adapt your styles based on validation. In the module about [CSS](https://web.dev/learn/forms/styling) you will learn more about styling forms.

## Validation with JavaScript

To further enhance validation of your forms you can use the [JavaScript Constraint Validation API](https://developer.mozilla.org/docs/Web/API/Constraint_validation).

### Provide meaningful error messages

You learned before that error messages are not identical in every browser. How can you show the same message to everyone?

To achieve this, use the [`setCustomValidity()`](https://developer.mozilla.org/docs/Web/API/HTMLObjectElement/setCustomValidity) method of the Constraint Validation API. Let's see how this works.

```
const nameInput = document.querySelector('[name="name"]');

nameInput.addEventListener('invalid', () => {
    nameInput.setCustomValidity('Please enter your name.');
 });
```

Query the element where you want to set the custom error message. Listen to the `invalid` event of your defined element. There you set the message with `setCustomValidity()`. This example shows the message `Please enter your name.` if the input is invalid.

  CodePen Embed - Learn forms – validationMessage  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

[Open the demo](https://codepen.io/web-dot-dev/pen/7ea31257d7cd8fc28792c7f5cdaba97b) in different browsers, you should see the same message everywhere. Now, try to remove the JavaScript and try again. You see the default error messages again.

There is much more you can do with the Constraint Validation API. You’ll find a detailed look at using [validation with JavaScript](https://web.dev/learn/forms/javascript#validation_with_javascript) in a later module.

How to validate in real-time You can add real-time validation in JavaScript by listening to the `onblur` event of a form control, and validate the input immediately when a user leaves a form field.

  CodePen Embed - Learn forms – real-time validation  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Click the form field in the [demo](https://codepen.io/web-dot-dev/pen/b7ed22a0539f9beef4dc03380f51f224), enter "web" and click somewhere else on the page. You see the native error message for `minlength` below the form field.

Learn more about implementing [real-time validation with JavaScript](https://web.dev/learn/forms/javascript#ensure_users_are_notified_about_errors_in_real_time) in an upcoming module.

### Check your understanding

Test your knowledge of validating forms

What attribute do you use to make form controls mandatory?

Is it possible to define your own error messages?

Yes, with the Constraint Validation API.

Yes, with the `message` HTML attribute.

Yes, with the `:invalid` CSS pseudo element.

An `<input>` with `type="email"` and the `required` attribute can be submitted:

If its value contains the word email.

If its value is a valid email address.

## Resources

*   [Disable the payment button once the form is submitted](https://web.dev/articles/codelab-payment-form-best-practices#step_4_disable_the_payment_button_once_the_form_is_submitted)
*   [Add CSS to make the form work better](https://web.dev/articles/codelab-sign-up-form-best-practices#step_2_design_for_mobile_and_desktop)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
