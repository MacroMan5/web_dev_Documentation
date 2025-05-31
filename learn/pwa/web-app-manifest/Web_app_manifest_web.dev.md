# Web app manifest  |  web.dev

**Source URL:** [https://web.dev/learn/pwa/web-app-manifest?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%2Fweb-app-manifest](https://web.dev/learn/pwa/web-app-manifest?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fpwa%2Fweb-app-manifest)  
**Last Updated:** 2025-05-23T00:57:10.259Z  
**Extracted:** 2025-05-31 16:58:10

---

# Glitch

[Skip to main content](#main-content)

## Web app manifest

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

*   On this page
*   [Adding a web app manifest to your PWA](#adding_a_web_app_manifest_to_your_pwa)
    *   [Linking to your manifest](#linking_to_your_manifest)
    *   [Debugging the manifest](#debugging_the_manifest)
    *   [For Chromium browsers](#for_chromium_browsers)
    *   [For Firefox](#for_firefox)
*   [Designing your PWA experience](#designing_your_pwa_experience)
    *   [Basic fields](#basic_fields)
    *   [Recommended fields](#recommended_fields)
    *   [Extended fields](#extended_fields)
    *   [Promotional fields](#promotional_fields)
    *   [Capabilities Fields](#capabilities_fields)
*   [Resources](#resources)

The web app manifest is a file you create that tells the browser how you want your web content to display as an app in the operating system. The manifest can include basic information such as the app's name, icon, and theme color; advanced preferences, such as desired orientation and app shortcuts; and catalog metadata, such as screenshots.

Each PWA should include a single manifest per application, typically hosted in the root folder, and linked on all HTML pages your PWA can be installed from. Its official extension is `.webmanifest`, so you could name your manifest something like `app.webmanifest`.

## Adding a web app manifest to your PWA

To create a web app manifest, first make a text file with a JSON object that contains at least a `name` field with a string value:

app.webmanifest:

```
{
   "name": "My First Application"
}
```

But creating the file is not enough, the browser needs to know it exists, too.

### Linking to your manifest

To make the browser aware of your web app manifest, you need to link it to your PWA using a `<link>` HTML element and the `rel` attribute set to `manifest` on all of your PWA's HTML pages. This is similar to how you link a CSS stylesheet to a document.

index.html:

```
<html lang="en">
  <title>This is my first PWA</title>
  <link rel="manifest" href="/app.webmanifest">
```

### Debugging the manifest

To ensure the manifest is set up correctly, you can use Inspector in Firefox and DevTools in every Chromium-based browser.

### For Chromium browsers

In DevTools

1.  In the left pane, under **Application**, select **Manifest**.
2.  Check the fields of the manifest as parsed by the browser.

### For Firefox

1.  Open the Inspector.
2.  Go to the Application tab.
3.  Select the Manifest option in the left panel.
4.  Check the fields of the manifest as parsed by the browser.

## Designing your PWA experience

With your PWA now connected to its manifest, it's time to fill out the rest of the fields to define the experience for your users.

### Basic fields

The first set of fields represents the core information about your PWA. They are used to build the installed PWA's icon and window and determine how it starts up. They are:

`name`

Full name of your PWA. It will appear along with the icon in the operating system's home screen, launcher, dock, or menu.

`short_name`

Optional, a shorter name of your PWA, used when there is not enough room to display the full value of the `name` field. Keep it under 12 characters to minimize the possibility of truncation.

`icons`

Array of icon objects with `src`, `type`, `sizes`, and optional `purpose` fields, describing what images should represent the PWA.

`start_url`

The URL the PWA should load when the user starts it from the installed icon. An absolute path is recommended, so if your PWA's home page is the root of your site, you could set this to ‘/' to open it when your app starts. If you don't provide a start URL, the browser can use the URL the PWA was installed from as a start. It can be a deep link, such as the details of a product instead of your home screen.

`display`

One of `fullscreen`, `standalone`, `minimal-ui`, or `browser`, describing how the OS should draw the PWA window. You can read more about the different display modes in the [App Design chapter](https://web.dev/learn/pwa/app-design#display_modes). [Most](https://almanac.httparchive.org/en/2021/pwa#top-manifest-display-values) use cases implement `standalone`.

`id`

A string that uniquely identifies this PWA against others that may be hosted on the same origin. If it's not set, the `start_url` will be used as a fallback value. Keep in mind that by changing the `start_url` in the future (such as when changing a query string value) you may be removing the browser's ability to detect that a PWA is already installed.

#### Icons

Your PWA's icon is its visual identity across your users' devices when installed, so it's important to define at least one. Because the `icons` property is a collection of icon objects, you can define several icons in different formats to provide the best icon experience for your users. Each browser will pick one or more icons based on its needs and the operating system it's installed on, the icons closer to the specifications needed.

If you need to pick only one icon size, it should be 512 by 512 pixels. However, providing more sizes is recommended including 192 by 192, 384 by 384, and 1024 by 1024 pixel-sized images, too.

```
"icons": [
   {
      "src": "icons/512.png",
      "type": "image/png",
      "sizes": "512x512"
   },
   {
      "src": "icons/1024.png",
      "type": "image/png",
      "sizes": "1024x1024"
   }
]
```

If you don't provide an icon or the icons are not in the recommended sizes, on some platforms you won't pass [installation criteria](https://web.dev/learn/pwa/installation#installation_criteria). On other platforms, the icon will be automatically generated, for instance from a screenshot of the PWA or by using a generic icon.

##### Maskable icons

Some operating systems, such as Android, adapt icons to different sizes and shapes. For example, on Android 12, different manufacturers or settings can change the shape of icons from circles to squares to rounded-corner squares. To support these kinds of adaptive icons, you can provide a maskable icon using the `purpose` field.

To do so, provide a square image file that has its main icon contained within a “safe zone”, a circle centered in the icon with a radius of 40 percent of the width of the icon. (See the image below.) Devices that support maskable icons will mask your icon as needed.

![The safe area marked as a 40 percent radius centered circle within the square icon](https://web.dev/static/learn/pwa/web-app-manifest/image/the-safe-area-marked-a-4-06cd30afb47b2.png)

Here's an example of a maskable icon rendered in a number of commonly used shapes:

In the following image, if you use the icon at the left as a maskable icon, you will end up with poor results on devices when a shape mask is applied.

![An icon that is not suitable for a maskable icon.](https://web.dev/static/learn/pwa/web-app-manifest/image/an-icon-is-suitable-a-554e022a4bec.png)

This image could be made usable with more padding.

![The icon with more padding is suitable for masks.](https://web.dev/static/learn/pwa/web-app-manifest/image/the-icon-more-padding-is-9057ce1028452.png)

Maskable icons should be 512 by 512 at least. With one created, you can add it to your `icons` collection to improve the experience for supported devices:

```
"icons": [
   {
      "src": "/icons/512.png",
      "type": "image/png",
      "sizes": "512x512"
   },
   {
      "src": "/icons/1024.png",
      "type": "image/png",
      "sizes": "1024x1024"
   },
   {
      "src": "/icons/512-maskable.png",
      "type": "image/png",
      "sizes": "512x512",
      "purpose": "maskable"
   },
]
```

In most cases, if your maskable icon isn't displaying well, you can improve it by adding more padding. [Maskable.app](https://maskable.app/) is a free online tool to test and create a maskable version of your icon.

If your icon serves general and maskable purposes, you can set the `purpose` field to `"any maskable"`. Refer to the [MDN Web App Manifest documentation](https://developer.mozilla.org/docs/Web/Manifest/icons#purpose) for details.

### Recommended fields

The next set of fields to include are ones that will improve your user's experience, even though they're not required for installability.

`theme_color`

Default color for the application, sometimes affecting how the OS displays the site (for instance, the window and title bar color on desktop, or the status bar color on mobile devices). This color can be overridden by the HTML `theme-color` `<meta>` element.

`background_color`

Placeholder color to display in the application's background before its stylesheet is loaded. Safari on iOS and iPadOS and most desktop browsers currently ignore this field.

`scope`

Changes the navigation scope of the PWA, allowing you to define what is and isn't displayed within the installed app's window. For example, if you link to a page outside of the scope, it will be rendered in an in-app browser instead of within your PWA window. This will not, however, change the scope of your service worker.

The next image shows how the `theme_color` field is used for the title bar on a desktop device when you install a PWA.

![The same PWA installed on desktop with a different theme color.](https://web.dev/static/learn/pwa/web-app-manifest/image/the-same-pwa-installed-d-584337198daf1.png)

When defining colors in the manifest, such as within `theme_color` and `background_color`, you should use CSS named colors, such as `salmon` or `orange`, RGB colors such as `#FF5500`, or color functions without transparency such as `rgb()` or `hsl()`. Check the [App design chapter](https://web.dev/learn/pwa/app-design#theming_your_app) for more information.

#### Try it

#### Splash screens

On some devices, a static image is rendered while your PWA is being loaded to provide immediate feedback to the user.

Android uses the `theme_color`, `background_color`, and `icon` values to generate the splash screen.

When you install a PWA on Android, the device will generate a splash screen with the information that comes from your manifest as seen in the following diagram.

![A PWA on Android splash screen taking different values from the manifest.](https://web.dev/static/learn/pwa/web-app-manifest/image/a-pwa-android-splash-scr-fb6e3edede13e.png)

Safari on iOS and iPadOS, on the other hand, doesn't use the web app manifest to generate splash screens. Instead, they use an image linked from a proprietary `<link>` element similar to how they handle icons. Check the [Enhancement chapter](https://web.dev/learn/pwa/enhancements) for more details.

### Extended fields

The next set of fields offers additional information about your PWA. They are all optional.

`lang`

A language tag specifying the primary language of the manifest's values, such as `en` for English, `pt-BR` for Brazilian Portuguese, or `in` for Hindi.

`dir`

The direction to display direction-capable manifest fields (such as `name`, `short_name`, and `description`). Valid values are `auto`, `ltr` (left-to-right), and `rtl` (right-to-left).

`orientation`

Desired orientation for the app once installed. A game may set this to request a landscape-only orientation. [Several values](https://developer.mozilla.org/docs/Web/Manifest/orientation#values) are accepted, but if included it's typically `portrait` or `landscape` explicitly.

### Promotional fields

The fourth set of fields lets you provide promotional information about your PWA, for instance, in install flows, listings, and search results.

`description`

An explanation of what the PWA does.

`screenshots`

Array of screenshot objects with `src`, `type`, and `sizes` (similar to the `icons` object) intended to showcase the PWA. There are no size restrictions.

`categories`

Array of categories the PWA should belong to be used as hints for listings, optionally from the list of [known categories](https://www.w3.org/TR/manifest-app-info/#categories-member). These values are typically lowercase.

`iarc_rating_id`

The International Age Rating Coalition certification code for the PWA, if you have one. It is intended to be used to determine which ages your PWA is appropriate for.

You can see these promotional fields in action today. On Android, for example, if your PWA is installable and you provide values for at least the `description` and `screenshots` fields, the installation dialog experience transforms from a simple "Add to the home screen" info bar, to a richer installation dialog similar to the one from an app store.

On Android, you can get a nicer installation UI if you provide values for the promotional fields, as you can see in the next video

See these promotional fields in action:

### Capabilities Fields

Finally, there are a number of fields related to different capabilities that your PWA can use in supported browsers, such as the `shortcuts`, `share_target`, `display_override` fields as we cover in the [Capabilities chapter](https://web.dev/learn/pwa/capabilities). There are also fields, like `related_apps` and `prefer_related_apps` (see the [Detection chapter](https://web.dev/learn/pwa/detection) for more information), to connect your PWA to installed apps, often from an app store.

Many new fields may appear in the future while browsers add more capabilities to Progressive Web Apps.

## Resources

*   [Add a Web App Manifest](https://web.dev/articles/add-manifest)
*   [Adaptive icon support in PWAs with maskable icons](https://web.dev/articles/maskable-icon)
*   [Richer PWA installation UI](https://developer.chrome.com/blog/richer-pwa-installation)
*   [MDN: Web App Manifest](https://developer.mozilla.org/docs/Web/Manifest)

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2024-12-09 UTC.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
