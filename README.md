# ChromeDevTool
Building a Chrome developers tool. Because its not like building a web page.

## Quickstart


Create a Manifest file called manifest.json.

Create an HTML file for your panel. Name it devtools.html.

Add this into your manifest.json

```
{
  "name": "A sample name",
  "version": "1.1",
  "description": "Some kind of description.",
  "devtools_page": "devtools.html",
  "manifest_version": 2
}
```

4. In devtools.html, add the following code:

```
<html>
<body>
<script src="devtools_page.js"></script>
</body>
</html>

```

5. Create a file called devtools_page.js and add the following code:

```
chrome.devtools.panels.create(
  'myInspector',
  '',
  'panel/panel.html'
);
```

6. Create a folder called panel. Inside of this folder create a file called panel.html.

7. In panel.html add the following:

```Hello, World```

8. Install [this](https://chrome.google.com/webstore/detail/chrome-apps-extensions-de/ohmmkhmmmpcnpikjeljgnaoabkaalbgc?hl=en) tool to help you make a Chrome extension.

9. Chrome > More tools > extensions and click on "Load unpacked extension".

10. Press Option + Command + J a few times until you see your extension.


## Next : Changing the DOM of your page

In your manifest, add a content script:

```
"content_scripts" : [{
      "matches" : ["<all_urls>"],
      "js" : ["content_script.js"],
      "run_at" : "document_end"
  }]
```

In the content_script, add some javascript.

```
var body = document.querySelector('body');
body.style.backgroundColor = "#FF0000"
```

Note: you might want to uninstall your extension after you try this.


## Advanced : getting your dev tool panel to talk with the inspected Window
So, your dev tool panel ("panel.html") needs to be able to communicate with whatever is going on in your inspected window.


## Tooling

Install node.

Then install gulp:

```
npm install --global gulp
```


## The manifest file
The manifest is a JSON file.

In your manifest, you describe your background pages, your content scripts, which scripts are available in the inspected window ("web accessible resources").

You also put the icons for your devtool here.


## Background page
The background page has access to the Chrome extension apis. 

If you want to manipulate or otherwise access DOM elements (like the body tag) of your inspected window, you can't do that in the background page. You have to use the background page to send a message to your content scripts

## Content scripts
Content scripts can access the DOM of a page and can listen to DOM events (like clicks).

If you want to inject css into the inspected window, this is a content script.


## Injected Scripts
Content scripts can not access any variables or functions of your inspected window. 

To access variables or functions of your inspected window, you have to use your content script to inject what's called an "injected script". 

Then you have to use ```window.sendMessage``` to send a message to the content script.