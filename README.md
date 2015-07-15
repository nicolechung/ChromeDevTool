# ChromeDevTool
Building a Chrome developers tool. Because its not like building a web page.

## Quickstart
1. Create a Manifest file called manifest.json.
2. Create an HTML file for your panel. Name it devtools.html.
3. Add this into your manifest.json

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