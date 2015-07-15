# ChromeDevTool
Building a Chrome developers tool



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

