# Test your forms  |  web.dev

**Source URL:** [https://web.dev/learn/forms/testing?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Ftesting](https://web.dev/learn/forms/testing?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fforms%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fforms%2Ftesting)  
**Last Updated:** 2025-05-23T00:59:11.338Z  
**Extracted:** 2025-05-31 16:58:10

---

# Test your forms | web.dev

In previous modules, you learned how to build a form, help users avoid re-entering data, and how to validate form data. How can you now make sure the form is usable? You can test and analyze your form to answer this question.

## Does your form work on other devices?

You begin by confirming that your form is working on your own device. However, there are many types of devices your users may use. How can you test if your form works with other devices?

First, test your form on a desktop device. Then try only using your keyboard. Next, test it on a phone. You have now tested your form with different input methods (keyboard, touch, and mouse), different screen sizes, different browsers and different operating systems.

Do you have more devices you can test on? Test your form on all of them. The more different devices, browsers, browser versions, and operating systems you can test on, the better!

You can also use a test service to test your form on lots of different browsers, different browser versions, different devices, and different operating systems. [BrowserStack](https://www.browserstack.com/) offers free test accounts for open source projects, to enable testing on different browsers, devices and operating systems.

## How can you test if your form works for others?

Your first form is ready. You spend a lot of time making sure it works well. How can you confirm that your form is usable for everybody else? As a first step, you can ask your friends and colleagues to fill out your form.

Sit next to each other or share a screen. This way, you can see how they interact with your form. Watch them fill out the form. Ask them to say out loud what they're doing and if they're experiencing any problems. After they complete the task, ask them questions. Was it clear what they should fill out? Did they have any issues filling out the form? Was anything unclear? These questions help you build even better forms.

## How can you measure how your form performs?

You confirmed that your form is usable for other people. As a next step, you should measure how your form performs. There are free tools available for this. Let's have a look at some of them.

### PageSpeed Insights (PSI)

PSI measures the performance of your site and gives you hints on how to improve it.

[Try it out](https://pagespeed.web.dev/): PageSpeed provides a performance report using [lab and field data](https://developers.google.com/speed/docs/insights/v5/about/). A fast site is the first sign that your form is usable. Your site isn't fast yet? PSI shows you recommendations on how to improve performance.

Look again at the report of your site you tested before with PSI. See the information about [Core Web Vitals](https://web.dev/articles/vitals)? This is a summary if your site fulfills the Core Web Vitals criteria. Core Web Vitals help you understand how users experience a web page.

### Lighthouse

Lighthouse helps you identify performance, search engine optimization (SEO), best practice, and accessibility issues.

There are different ways to use [Lighthouse](https://developer.chrome.com/docs/lighthouse/overview). One option is to run it directly in [DevTools](https://developer.chrome.com/docs/lighthouse/overview#devtools). Open the URL with your form in Chrome, [open DevTools](https://developer.chrome.com/docs/devtools/shortcuts#open), switch to the Lighthouse tab, and run the audit.

The performance metrics from PSI are displayed. In addition, Lighthouse checks your site against SEO, best practice, and accessibility issues. Forgot to connect a label to a form control? Lighthouse warns you and provides you with a guide to correct the issue.

### Tools to identify common issues

There are many tools to identify common issues. One way is to use the [Form troubleshooter extension](https://chrome.google.com/webstore/detail/form-troubleshooter/lpjhcgjbicfdoijennopbjooigfipfjh). It warns you about missing `autocomplete` attributes, non-standard attributes, missing or empty labels, and more.

You can also use an accessibility evaluation tool like [WAVE](https://wave.webaim.org/) or [axe](https://www.deque.com/axe/). These tools notify you about missing labels, missing connections between labels and form controls, insufficient color contrasts, and many more accessibility issues.

## How can you monitor form experience?

Monitoring real user experience of your forms helps you identify new issues quickly. Let's see how you can monitor your form.

### PSI

One way to monitor experience is to use PSI again. You can use the [PSI API](https://developers.google.com/speed/docs/insights/v5/get-started) to build your own monitoring tool: [The PageSpeed Insights API](https://addyosmani.com/blog/pagespeed-insights-api/) explains how to do this.

PSI includes data from the [Chrome User Experience Report](https://developer.chrome.com/docs/crux) (CrUX) dataset, if available for the given URL. This way, you can also see field data directly in the report.

### Lighthouse

Lighthouse can be used as a command line tool, as a [Node module](https://www.npmjs.com/package/lighthouse), or with the [Lighthouse CI tools](https://github.com/GoogleChrome/lighthouse-ci). [Performance monitoring with the Lighthouse CI](https://web.dev/articles/lighthouse-ci) explains adding Lighthouse to a continuous integration system, such as GitHub Actions.

There are many more [tools](https://web.dev/vitals-tools-workflow) available to measure and monitor your site. Some are available as web tools, some let you run the audit on your command line, and some offer an API to integrate them into your tools.

## How to analyze your form

You tested your form with real users, and learned how to measure and monitor it. How can you collect statistics about your users and how they interact with your form? You can use an analytics tool. Let's have a look at one and how this works.

### Analytics

One tool you can use is [Google Analytics](https://developers.google.com/analytics) (GA). After setting it up, you get a JavaScript snippet you include in each page on your site. From this point on, you can find out how people use your site.

How many people visit the page with your form on it? How many fill out the form and move to the next page? You get answers to these questions by using analytics tools.

You can also set up more advanced analytics reports. Want to track how many users click the **Submit** button? You can define and integrate [events](https://developers.google.com/analytics/devguides/collection/gtagjs/events) to analyze this.

A wide range of analytics tools is available. Some are minimalistic, some offer a lot of options for individualization. Try out a range of tools to find the best for your needs.

### Check your understanding

Test your knowledge of testing forms

What is field data?

Data from real conditions.

Data collected on a field.

RUM collects metrics from:

## Resources

*   [Getting started with measuring Web Vitals](https://web.dev/articles/vitals-measurement-getting-started)
*   [Core Web Vitals](https://web.dev/articles/vitals)
*   [Why lab and field data can be different](https://web.dev/articles/lab-and-field-data-differences)
*   [Google Analytics: About Events](https://support.google.com/analytics/answer/1033068#zippy=%2Cin-this-article)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
