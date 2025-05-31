# Security and privacy  |  web.dev

**Source URL:** [https://web.dev/learn/forms/security-privacy?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fsecurity-privacy](https://web.dev/learn/forms/security-privacy?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Fsecurity-privacy)  
**Last Updated:** 2025-05-23T00:59:55.263Z  
**Extracted:** 2025-05-31 16:58:10

---

# Security and privacy | web.dev

When you create a form, you work with user data. Your number one concern should be to ensure that user data is kept private and transferred securely. Let's have a look at what can be done.

## Ensure your form is secure

As a first step, make sure to request as little data as possible. Don't ask for data you don't need, and always question whether you need all of the requested data. Less data means less risk, less cost, and less liability. In addition, reducing the number of fields in a form makes it less complex, easier to fill out, and can reduce abandonment rates.

[Always use HTTPS](https://web.dev/explore/secure#secure-connections-with-https), especially for pages that include a form. With HTTPS, data is encrypted when coming from the server and when going back to the server.

Say you're sitting in a café using public Wi-Fi. You open an ecommerce site and fill in your credit card information to purchase something. If the website uses HTTP, anyone (with the skills to do so) on the same public Wi-Fi could see your credit card information. If the website uses HTTPS, the data is encrypted and therefore protected from anyone trying to access it.

On your site, you should also make sure to redirect any HTTP requests to HTTPS. Learn more about [how to redirect all traffic to HTTPS](https://geekflare.com/http-to-https-redirection/).

## Help users to keep their data private

In the [first module](https://web.dev/learn/forms/form-element), you learned about two possible ways to transfer data: using a `GET` request and using a `POST` request.

With a `GET` request, form data is included as a [query string](https://en.wikipedia.org/wiki/Query_string) in the request URL. If you submit a form that uses a `GET` request, the browser adds the request URL including form data to your browsing history. Convenient if you want to look up past form submissions, for example for a search form. Not great at all, if sensitive data is submitted, and everybody with access to your browser history or local network can see this information.

Use `POST` requests for every form where data that's personal or otherwise sensitive may be submitted. This way, the data is only visible to the backend script processing it.

What about saving and processing personal data directly in the browser? You could use client storage, for example, `localStorage` to store personal data in the browser. With regard to privacy, this is less than ideal. Again, everyone with access to your browser is able to read this information. You should only store encrypted values for personal data.

## Ensure users can safely sign up and sign in

User account [authentication](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html) is a complex issue in terms of privacy and security. It may be better to use a [third-party identity provider](https://web.dev/articles/sign-up-form-best-practices#federated-login), instead of building your own secure authentication system.

Learn more about [best practices for account authentication, and password management](https://cloud.google.com/blog/products/identity-security/account-authentication-and-password-management-best-practices).

## Help users access their personal data

Many regions have laws and regulations regarding data protection and privacy, including the [CCPA](https://en.wikipedia.org/wiki/California_Consumer_Privacy_Act) in California and the [PDPA](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3244203) in India. Every website available in the European Union (EU) has to follow [General Data Protection Regulation](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation) (GDPR), even if the site is not based in the EU.

GDPR sets guidelines for the collection and processing of personal information from people living in the EU. Consent is required to process personal data, users can request personal information that you store at any time, and you have to officially announce data leaks. A good thing for the user, as this helps to ensure that their privacy is respected. Learn more about [GDPR](https://www.smashingmagazine.com/2018/02/gdpr-for-web-developers/).

Make sure your users know how you plan to process personal data. Transparency is the key to trust. Users should always be able to access, modify, and delete all data you saved for them.

## Ensure users can update their personal data

Make it easy for users to update their personal data, including passwords, email addresses, and usernames. Notify users about changes to their stored personal data, and ensure users can revoke changes. For example, send an email to the previous and new email address after users change their email address.

Make it easy for users to delete their account, including all associated data, and where relevant, make it possible to download data. Account deletion is a [legal requirement](https://ec.europa.eu/info/law/law-topic/data-protection_en) in some regions.

Require an additional authentication step, for example, re-entering the current password, to view or change personal information on your site.

Find out more: [Web Application Privacy Best Practices](https://www.w3.org/TR/app-privacy-bp/).

## Ensure all data is in good shape

In a previous module, you learned about [validation on the frontend](https://web.dev/learn/forms/validation). Frontend validation is important, but users might still be able to submit invalid data. As a next step, you must also validate the data [on the backend](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html) before saving the data in your database. This ensures that no invalid data is saved in your database.

Validation helps to ensure that the data format is valid, but you should still not trust data entered by users. How can you safely output the data? To prevent [Cross Site Scripting](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html) (XSS), and ensure all data is safe to include in HTML, you must sanitize data before output.

Learn more about [sanitizing data before output](https://benhoyt.com/writings/dont-sanitize-do-escape/) and, where possible, use the [Sanitizer API](https://web.dev/articles/sanitizer).

## Ensure all submissions come from real people

To help protect your data, you have various options to prevent spam submissions from [bots](https://en.wikipedia.org/wiki/Internet_bot#Malicious_bots).

The first option is to use a service such as [reCAPTCHA](https://www.google.com/recaptcha/about/), to distinguish between real people and bots. This requires you to include a JavaScript snippet on your page, and add extra attributes to your **Submit** button.

reCAPTCHA performs various checks to find out if you are a human. For example, it may ask you to identify images. Automated software, such as a bot, cannot accomplish these challenges and can't submit the form.

### A honeypot

  CodePen Embed - Learn forms – honeypot spam protection  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Another option is to use a so-called 'honeypot': a visually hidden form field. Humans won't see a honeypot field, but bots will fill it in. On the backend, your processing script can check if the field was completed. If it was, the submission was probably from a bot, and you can ignore it.

There are also services like [Akismet](https://akismet.com/), which can help you with spam protection. The Akismet filter works by combining information about spam captured on all participating sites, and then using those spam rules to block future spam. Akismet is transparent to the user, and catches most spam.

### Check your understanding

Test your knowledge of security and privacy

What is the preferred method to transfer personal data using forms?

How can you prevent spam?

Only serve vegetarian forms.

## Resources

*   [Digital Identity Guidelines](https://pages.nist.gov/800-63-3/sp800-63b.html)
*   [Database Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Database_Security_Cheat_Sheet.html)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
