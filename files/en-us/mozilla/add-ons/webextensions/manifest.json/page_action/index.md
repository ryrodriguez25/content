---
title: page_action
slug: Mozilla/Add-ons/WebExtensions/manifest.json/page_action
page-type: webextension-manifest-key
browser-compat: webextensions.manifest.page_action
sidebar: addonsidebar
---

<table class="fullwidth-table standard-table">
  <tbody>
    <tr>
      <th scope="row">Type</th>
      <td><code>Object</code></td>
    </tr>
    <tr>
      <th scope="row">Mandatory</th>
      <td>No</td>
    </tr>
    <tr>
      <th scope="row">Manifest version</th>
      <td>2 or higher</td>
    </tr>
    <tr>
      <th scope="row">Example</th>
      <td>
        <pre class="brush: json">
"page_action": {
  "default_icon": {
    "19": "button/geo-19.png",
    "38": "button/geo-38.png"
  },
  "default_title": "Whereami?",
  "default_popup": "popup/geo.html"
}</pre
        >
      </td>
    </tr>
  </tbody>
</table>

A page action is an icon that your extension adds inside the browser's URL bar.

Your extension may optionally also supply an associated popup whose content is specified using HTML, CSS, and JavaScript.

You must specify this key to include a page action in your extension. When specified, you can manipulate the button programmatically using the {{WebExtAPIRef("pageAction")}} API.

If you supply a popup, then the popup is opened when the user clicks the icon, and your JavaScript running in the popup can handle the user's interaction with it. If you don't supply a popup, then a click event is dispatched to your extension's [background scripts](/en-US/docs/Mozilla/Add-ons/WebExtensions/Anatomy_of_a_WebExtension#background_scripts) when the user clicks the icon.

Page actions are like browser actions, except that they are associated with particular web pages rather than with the browser as a whole. If an action is only relevant on certain pages, then you should use a page action and display it only on relevant pages. If an action is relevant to all pages or to the browser itself, use a browser action.

While browser actions are displayed by default, page actions are hidden by default. They can be shown for a particular tab by calling {{WebExtAPIRef("pageAction.show()")}}, passing in the tab's `id`. You can also change this default behavior using the `show_matches` property.

## Syntax

The `page_action` key is an object that may have any of three properties, all optional:

<table class="fullwidth-table standard-table">
  <thead>
    <tr>
      <th scope="col">Name</th>
      <th scope="col">Type</th>
      <th scope="col">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <code>
          <a href="/en-US/docs/Mozilla/Add-ons/WebExtensions/user_interface/Browser_styles">
            browser_style
          </a>
        </code>
        <br />{{optional_inline}}
        <br />{{deprecated_inline}} in Manifest V3.
      </td>
      <td><code>Boolean</code></td>
      <td>
        <p>Optional. Defaults to <code>false</code>.</p>
        <div class="notecard warning">
          <p>
            Do not set <code>browser_style</code> to true: its not support in Manifest V3 from Firefox 118. See <a href="/en-US/docs/Mozilla/Add-ons/WebExtensions/user_interface/Browser_styles#manifest_v3_migration">Manifest V3 migration for <code>browser_style</code></a>.
          </p>
        </div>
        <p>
          In Firefox, the stylesheet can be seen at
          <code>chrome://browser/content/extension.css</code> or
          <code>chrome://browser/content/extension-mac.css</code> on macOS.
        </p>
        <p>
          The
          <a
            href="https://github.com/mdn/webextensions-examples/tree/main/latest-download"
            >latest-download</a
          >
          example extension uses <code>browser_style</code> in its popup.
        </p>
      </td>
    </tr>
    <tr>
      <td><code>default_icon</code></td>
      <td><code>Object</code> or <code>String</code></td>
      <td>
        <p>Use this to specify an icon for the action.</p>
        <p>
          It's recommended that you supply two icons here (19×19 pixels and
          38×38 pixels), and specify them in an object with properties named
          <code>"19"</code> and <code>"38"</code>, like this:
        </p>
        <pre class="brush: json">
    "default_icon": {
      "19": "geo-19.png",
      "38": "geo-38.png"
    }</pre
        >
        <p>
          If you do this, then the browser will pick the right size icon for the
          screen's pixel density.
        </p>
        <p>You can just supply a string here:</p>
        <pre class="brush: json">"default_icon": "geo.png"</pre>
        <p>
          If you do this, then the icon will be scaled to fit the toolbar, and
          may appear blurry.
        </p>
      </td>
    </tr>
    <tr>
      <td><code>default_popup</code></td>
      <td><code>String</code></td>
      <td>
        <p>
          The path to an HTML file containing the specification of the popup.
        </p>
        <p>
          The HTML file may include CSS and JavaScript files using
          <code
            ><a href="/en-US/docs/Web/HTML/Reference/Elements/link">&#x3C;link></a></code
          >
          and
          <code
            ><a href="/en-US/docs/Web/HTML/Reference/Elements/script"
              >&#x3C;script></a
            ></code
          >
          elements, just like a normal web page. However, don't use
          <code
            ><a href="/en-US/docs/Web/HTML/Reference/Elements/script"
              >&#x3C;script></a
            ></code
          >
          with embedded code, because you'll get a Content Violation Policy
          error. Instead,
          <code
            ><a href="/en-US/docs/Web/HTML/Reference/Elements/script"
              >&#x3C;script></a
            ></code
          >
          must use the
          <code><a href="/en-US/docs/Web/HTML/Reference/Elements/script">src</a></code>
          attribute to load a separate script file.
        </p>
        <p>
          Unlike a normal web page, JavaScript running in the popup can access
          all the
          <a href="/en-US/docs/Mozilla/Add-ons/WebExtensions/API"
            >WebExtension APIs</a
          >
          (subject, of course, to the extension having the appropriate
          <a
            href="/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/permissions"
            >permissions</a
          >).
        </p>
        <p>
          This is a
          <a
            href="/en-US/docs/Mozilla/Add-ons/WebExtensions/Internationalization#internationalizing_manifest.json"
            >localizable property</a
          >.
        </p>
      </td>
    </tr>
    <tr>
      <td><code>default_title</code></td>
      <td><code>String</code></td>
      <td>
        <p>
          Tooltip for the icon, displayed when the user moves their mouse over
          it.
        </p>
        <p>
          This is a
          <a
            href="/en-US/docs/Mozilla/Add-ons/WebExtensions/Internationalization#internationalizing_manifest.json"
            >localizable property</a
          >.
        </p>
      </td>
    </tr>
    <tr>
      <td><code>hide_matches</code></td>
      <td>
        <code>Array</code> of <code>Match Pattern</code> except
        <code>&#x3C;all_urls></code>
      </td>
      <td>
        <p>
          Hide the page action by default for pages whose URLs match any of the
          given
          <a href="/en-US/docs/Mozilla/Add-ons/WebExtensions/Match_patterns"
            >match patterns</a
          >.
        </p>
        <p>
          Note that page actions are always hidden by default unless
          <code>show_matches</code> is given. Therefore, it only makes sense to
          include this property if <code>show_matches</code> is also given, and
          will override the patterns in <code>show_matches</code>.
        </p>
        <p>For example, consider a value like:</p>
        <pre class="brush: json">
"page_action": {
  "show_matches": ["https://*.mozilla.org/*"],
  "hide_matches": ["https://developer.mozilla.org/*"]
}</pre
        >
        <p>
          This shows the page action by default for all HTTPS URLs under the
          <code>"mozilla.org"</code> domain, except for pages under
          <code>"developer.mozilla.org"</code>.
        </p>
      </td>
    </tr>
    <tr>
      <td><code>show_matches</code></td>
      <td><code>Array</code> of <code>Match Pattern</code></td>
      <td>
        <p>
          Show the page action by default for pages whose URLs match any of the
          given patterns.
        </p>
        <p>See also <code>hide_matches</code>.</p>
      </td>
    </tr>
    <tr>
      <td><code>pinned</code> {{deprecated_inline}}</td>
      <td><code>Boolean</code></td>
      <td>
        <p>Optional. Defaults to <code>true</code>.</p>
        <p>
          Controls whether or not the page action should appear in the location
          bar by default when the user installs the extension. This property is
          no longer supported since Firefox 89.
        </p>
      </td>
    </tr>
  </tbody>
</table>

## Example

```json
"page_action": {
  "default_icon": {
    "19": "button/geo-19.png",
    "38": "button/geo-38.png"
  }
}
```

A page action with just an icon, specified in 2 different sizes. The extension's background scripts can receive click events when the user clicks the icon using code like this:

```js
browser.pageAction.onClicked.addListener(handleClick);
```

```json
"page_action": {
  "default_icon": {
    "19": "button/geo-19.png",
    "38": "button/geo-38.png"
  },
  "default_title": "Whereami?",
  "default_popup": "popup/geo.html"
}
```

A page action with an icon, a title, and a popup. The popup will be shown when the user clicks the icon.

## Browser compatibility

{{Compat}}

## See also

- [`browser_action`](/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/browser_action)
- [`sidebar_action`](/en-US/docs/Mozilla/Add-ons/WebExtensions/manifest.json/sidebar_action)
- [Browser styles](/en-US/docs/Mozilla/Add-ons/WebExtensions/user_interface/Browser_styles)
