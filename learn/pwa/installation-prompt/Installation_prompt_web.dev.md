# Installation prompt  |  web.dev

**Source URL:** [https://web.dev/learn/pwa/installation-prompt?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%2Finstallation-prompt](https://web.dev/learn/pwa/installation-prompt?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%2Finstallation-prompt)  
**Last Updated:** 2025-05-23T00:57:21.248Z  
**Extracted:** 2025-05-31 16:58:10

---

# Glitch

Installation prompt

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

Users may not be familiar with the PWA install process. As the developer, you will understand when it is the right time to invite the user to install the app. The default browser installation prompts can also be enhanced. Let's check out the tools available.

## Enhancing the install dialog

Browsers provide default installation prompts when PWAs pass the install criteria. The browser uses the `name` and `icons` properties from your [Web App Manifest](https://web.dev/learn/pwa/web-app-manifest) to build the prompt.

![Microsoft Edge installation prompt.](https://web.dev/static/learn/pwa/installation-prompt/image/microsoft-edge-installati-78781d84f37f.png)

Some browsers enhance the installation prompt experience using the [promotional fields in the manifest](https://web.dev/learn/pwa/web-app-manifest#promotional_fields), including `description`, `categories`, and `screenshots`. For example, using Chrome on Android, if your PWA provides values for the `description` and `screenshots` fields, the installation dialog experience transforms from a small **Add to home screen** info bar to a bigger, more detailed dialog, similar to the install prompts from an app store.

See promotional fields in action:

## The beforeinstallprompt event

The browser's installation prompts are the first step in getting users to install your PWA. To implement your own install experience, your app still needs to pass the install criteria: when the browser detects that your app is installable, it fires the `beforeinstallprompt` event. You need to implement this event handler to customize the user's experience. Here's how:

1.  Listen for the `beforeinstallprompt` event.
2.  Save it (you'll need it later).
3.  Trigger it from your UI.

Check the code below for an example of an event listener for the `beforeinstallprompt` event, its capture and later custom use.

```
// This variable will save the event for later use.
let deferredPrompt;
window.addEventListener('beforeinstallprompt', (e) => {
  // Prevents the default mini-infobar or install dialog from appearing on mobile
  e.preventDefault();
  // Save the event because you'll need to trigger it later.
  deferredPrompt = e;
  // Show your customized install prompt for your PWA
  // Your own UI doesn't have to be a single element, you
  // can have buttons in different locations, or wait to prompt
  // as part of a critical journey.
  showInAppInstallPromotion();
});
```

Then, if the user clicks on your customized install button, use the `deferredPrompt` that has previously been saved and call its `prompt()` method, because the user still needs to go through the browser's process to install your app. What you did was delay the event until you gave the user the right context to encourage them to install the PWA.

Capturing the event gives you the opportunity to add hints and incentives for your users to install your app, and to choose to prompt for installation when you know the users are more engaged.

The event will not fire if:

*   The user has already installed the current PWA (valid only for desktop and WebAPK on Android).
*   The app does not pass the [PWA installation criteria](https://web.dev/learn/pwa/installation#installation_criteria).
*   The PWA is not installable on the current device for other reasons (for example, a device in kiosk mode or without permissions).

### The best place to prompt

Where to prompt depends on your application and when your users are most engaged with your content and services. When you capture the `beforeinstallprompt`, you can guide users through the reasons to keep using your app and the advantages they will gain from installing it. You can choose to display install hints anywhere in your app. Some common patterns are: in the side menu, after a critical user journey such as completing an order, or after a sign-up page. You can read more about this in [Patterns for promoting PWA installation](https://web.dev/articles/promote-install).

### Gathering analytics

Using analytics will help you to understand better where and when to present your prompts. You can use the `userChoice` property from the `beforeinstallprompt` event; `userChoice` is a promise that will resolve with the action the user took.

```
// Gather the data from your custom install UI event listener
installButton.addEventListener('click', async () => {
  // deferredPrompt is a global variable we've been using in the sample to capture the `beforeinstallevent`
  deferredPrompt.prompt();
  // Find out whether the user confirmed the installation or not
  const { outcome } = await deferredPrompt.userChoice;
  // The deferredPrompt can only be used once.
  deferredPrompt = null;
  // Act on the user's choice
  if (outcome === 'accepted') {
    console.log('User accepted the install prompt.');
  } else if (outcome === 'dismissed') {
    console.log('User dismissed the install prompt');
  }
});
```

### See it in action

Try the following sample in action on a Chromium browser (desktop or Android).

## Fallback

If the browser doesn't support the `beforeinstallprompt` or the event does not fire, there is no other way to trigger the browser's installation prompt. However, on platforms that allow the user to install PWAs manually, like iOS, you can display these instructions to the user.

You should only render these instructions in browser mode; other display options, such as `standalone` or `fullscreen` mean the user has already installed the app.

To render the element only in browser mode, use the `display-mode` media query:

```
#installInstructions {
   display: none
}
@media (display-mode: browser) {
   #installInstructions {
     display: block
   }
}
```

## Codelab

## Libraries

Check out these libraries for help with rendering a custom install prompt:

*   [PWA Builder](https://github.com/pwa-builder/pwa-install)
*   [PWA Installer Prompt for React](https://github.com/shnaveen25/react-pwa-installer-prompt)
*   [React PWA Install](https://www.npmjs.com/package/react-pwa-install)
*   [Vue PWA Install](https://github.com/Bartozzz/vue-pwa-install)
*   [Add to Home Screen](https://github.com/docluv/add-to-homescreen)

## Resources

*   [Patterns for Promoting PWA installation](https://web.dev/articles/promote-install)
*   [How to provide your own in-app install experience](https://web.dev/articles/customize-install)
*   [MDN: Add to Home Screen](https://developer.mozilla.org/docs/Web/Progressive_web_apps/Add_to_home_screen)
*   [Web Manifest Incubations](https://wicg.github.io/manifest-incubations/)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
