# Identity  |  web.dev

**Source URL:** [https://web.dev/learn/forms/identity?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fidentity](https://web.dev/learn/forms/identity?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fidentity)  
**Last Updated:** 2025-05-23T01:00:55.955Z  
**Extracted:** 2025-05-31 16:58:10

---

# Identity  |  web.dev

Identity

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

## Help users sign up

The sign-up form is often the first interaction with a form on your website. Good sign-up form design is critical, and a secure form is essential.

Let's look at a sign-up form, and how you can help users sign up on your website.

  CodePen Embed - Learn forms – sign-up form  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Keep the sign-up form minimal and only show the required form controls to create an account. Don't double up your form controls to help users get their account details right. Send a confirmation email instead.

### Help users fill in their account details

You can help users fill in their account details by using the appropriate `autocomplete` attribute. Use `autocomplete="email"` for the email field, and `autocomplete="new-password"` for a new-password field.

Learn more about [autofilling input controls](https://web.dev/learn/forms/autofill).

You can also help users enter a secure password by offering a reveal-password `<button>`.  
Learn more about the [reveal-password pattern](https://web.dev/learn/forms/javascript#ensure_users_can_see_the_password_they_entered).

### Ensure your sign-up form is secure

Never store or transmit passwords in plain text. Make sure to [salt and hash](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html#Use_a_cryptographically_strong_credential-specific_salt) passwords—and [don't try to invent your own hashing algorithm](https://www.schneier.com/blog/archives/2011/04/schneiers_law.html).

Offer [multi-factor authentication](https://cheatsheetseries.owasp.org/cheatsheets/Multifactor_Authentication_Cheat_Sheet.html), especially if you store personal or sensitive data. [SMS OTP best practices](https://web.dev/articles/sms-otp-form) and [Enabling Strong Authentication with WebAuthn](https://developer.chrome.com/blog/webauthn) explain how to implement multi-factor authentication.

Ensure users don't use compromised passwords. For example, use the API from [Have I Been Pwned](https://haveibeenpwned.com/API/) to detect compromised passwords, and suggest your users fill in a different new password, or warn them if their password becomes compromised.

## Help users sign in

Let's see how to build a sign-in form to ensure users can easily sign in to your website.

  CodePen Embed - Learn forms – sign-in form  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Make the location of sign-up and sign-in buttons obvious. Ensure your form is usable on touch devices:

*   The [tap target size](https://web.dev/articles/accessible-tap-targets) of buttons is at least 48px.
*   The `font-size` of your form elements is big enough (`20px` is about right on mobile).
*   There is enough space (`margin`) between form controls, and that inputs are large enough (use at least `padding: 15px` on mobile).

### Help users fill in their email and password

Help browsers and password managers autofill account details. Use `autocomplete="email"` for the email field, and `autocomplete="current-password"` for a current password field.

To help users manually fill in their account details, use `type="email"` for the email field to show the appropriate on-screen keyboard on mobile devices.

Use the `required` attribute for your email and password field so you can warn of invalid values when the user submits the form. Consider using [real-time validation](https://web.dev/learn/forms/javascript#ensure_users_are_notified_about_errors_in_real_time) to help users correct invalid data as soon as they have entered it, rather than waiting for form submission.

### Ensure users can see the password they entered

The text you fill in for `<input type="password">` is obscured by default, to respect the privacy of users. Help users to enter their password, by showing a `<button>` to toggle the visibility of the entered text.

  CodePen Embed - Learn forms – reveal password  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Learn more about [implementing a password-reveal `<button>`](https://web.dev/learn/forms/javascript#ensure_users_can_see_the_password_they_entered).

## Ensure your sign-in and sign-up forms are usable

Test your sign-in and sign-up forms regularly with real people to make sure that authentication works as expected. Use analytics and [real user measurement (RUM)](https://web.dev/articles/user-centric-performance-metrics) to collect field data, and tools such as [Lighthouse](https://developer.chrome.com/docs/lighthouse/overview) and [PageSpeed Insights](https://pagespeed.web.dev/) to run tests yourself. Learn more about [testing for usability](https://web.dev/learn/forms/usability-testing) and [gathering analytics data](https://web.dev/learn/forms/data).

Ensure your forms work in different browsers and on different platforms. Test your form on different screen sizes, using only your keyboard, or using a screen reader such as [VoiceOver](https://www.youtube.com/watch?v=5R-6WvAihms&list=PLNYkxOF6rcICWx0C9LVWWVqvHlYJyqw7g&index=6) on Mac or [NVDA](https://www.nvaccess.org/) on Windows.

## Help users change their account settings

Make sure that users can change every account setting, including email addresses, passwords, and usernames.

Make it transparent what data you are storing, and help users download all their personal data at any time. Ensure users can delete their account if that's what they want. Account management features such as these may be a legal requirement in some regions.

### Ensure users can update their passwords

Make it easy for users to update their password.

  CodePen Embed - Learn forms – update password form  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Ask users for the current password before changing it, and send an email about a password change with the option to revert and lock the account.

Add the option to request a new password, and consider providing a [`.well-known` URL](https://web.dev/articles/change-password-url) for requesting a new password.

## Resources

*   [Password Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)
*   [Understanding the root cause of account takeover](https://security.googleblog.com/2017/11/new-research-understanding-root-cause.html)
*   [Password security: Complexity vs. length](https://resources.infosecinstitute.com/topic/password-security-complexity-vs-length/)
*   [Sign-up form best practices](https://web.dev/articles/sign-up-form-best-practices)
*   [Sign-in form best practices](https://web.dev/articles/sign-in-form-best-practices)
*   [Effective password management | Session](https://www.youtube.com/watch?v=4Ve2kw_AN84)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
