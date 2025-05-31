# Internationalization and localization  |  web.dev

**Source URL:** [https://web.dev/learn/forms/internationalization?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Finternationalization](https://web.dev/learn/forms/internationalization?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Finternationalization)  
**Last Updated:** 2025-05-23T00:59:48.237Z  
**Extracted:** 2025-05-31 16:58:10

---

# Internationalization and localization | web.dev

If you're reading this, you're using the World Wide Web. Your forms may be used by people speaking different languages, people from different countries, and people with different cultural backgrounds. Learn how to prepare your form for internationalization and localization.

## Ensure your form works in different languages

Let's see how you can make sure your form works with different languages.

The first step to make your site localization-ready is to define the language attribute `lang` on the `<html>` element. This attribute enables screen readers to invoke the correct pronunciation, and helps browsers offer a translation of the page if the defined language is not the default browser language.

```
<html lang="en-us">
```

Learn more about the [`lang`](https://developer.mozilla.org/docs/Web/HTML/Global_attributes/lang) attribute.

Say you translated a form to German. How can you make sure search engines and browsers know about the translated version? You can add `<link>` elements in your site's `<head>` describing the alternate versions.

```
<link rel="alternate" title="The form element"
  href="https://example.com/en/form" hreflang="en">
<link rel="alternate" title="Das Formularelement"
  href="https://example.com/de/form" hreflang="de">
```

## Help users who speak another language to use your form

You can't translate your form into every language, but you can ensure translation tools can translate it for you.

To ensure translation tools translate all the text on your form, make sure all text is defined in HTML and is visible. Some tools also work with content defined in JavaScript, but to improve compatibility, try to include as much text as possible in HTML.

## Ensure your form works with different writing systems

Different languages use different writing systems and character sets. Some scripts are written from left to right, and some from right to left.

### Make spacing independent of writing systems

To ensure your form works for different writing systems, you can use [CSS logical properties](https://developer.mozilla.org/docs/Web/CSS/CSS_Logical_Properties).

  CodePen Embed - Learn forms – logical properties  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

The input has a border thickness of `1px` on all sides, except on the left side, where the border is `4px` thick. Now, edit the [CodePen](https://codepen.io/web-dot-dev/pen/043b19ee429ea0834022967e2207d6b9) and change the writing system to right to left by adding `dir="rtl"` to the `<main>` element

The thick border is now on the right side. That's because we defined the border using a logical property.

```
input {
  border-inline-start-width: 4px;
}
```

Learn more about [logical properties](https://web.dev/learn/css/logical-properties).

## Ensure your form can handle different name formats

Say you have a form where the user should fill in their name. How would you add the field to your form?

You could add one field for the first name and one for the surname. However, names are different around the world: for example, some people don't have a surname—so how should they fill in the surname field?

To make it quick and easy to enter names—and to ensure everybody can enter their name, whatever the format—use a single form field for names wherever possible.

Learn more about [personal names](https://www.w3.org/International/questions/qa-personal-names).

If you have a name with [non-Latin characters](https://web.dev/articles/payment-and-address-form-best-practices#unicode-matching), you may have encountered the issue that your name is reported as `invalid` in some forms. When you build forms, make sure to allow all possible characters—and do not assume that a name only consists of Latin characters.

## Allow a variety of address formats

The headquarters of Google is at 1600 Amphitheatre Parkway, Mountain View, CA 94043, United States.

This address includes the street number, street, city, state, postal code, and country. In your country, the address format may be totally different. How can you ensure everybody can enter their address in your form?

One way is to use generic inputs.

  CodePen Embed - Learn forms – generic address  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

Learn more about other ways to work with [international address fields](https://www.uxmatters.com/mt/archives/2008/06/international-address-fields-in-web-forms.php).

### Check your understanding

Test your knowledge of internationalization and localization

How do you invoke the correct pronunciation for screen readers?

With the `hreflang` attribute.

With the `language` attribute.

Adding a description with what language is used.

How can you change the writing system on your website?

Using the `<link>` element.

Using CSS logical properties.

With the `direction` attribute.

## Resources

*   [W3C Internationalization articles and tutorials](https://www.w3.org/International/articlelist)
*   [Frank's Compulsive Guide to Postal Addresses](http://www.columbia.edu/%7Efdc/postal/) provides useful links and extensive guidance for address formats in over 200 countries.
*   [DataHub.io](https://datahub.io/core/country-list) is a tool for downloading country codes and names.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
