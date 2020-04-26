# Content Scripts

By default, runs after page has loaded in an isolated world with seperate variables but accessing same DOM

Use messages to access most chrome APIS, but can accessjj: 

- [i18n](https://developer.chrome.com/extensions/i18n)
- [storage](https://developer.chrome.com/extensions/storage)
- runtime:
  - [connect](https://developer.chrome.com/extensions/runtime#method-connect)
  - [getManifest](https://developer.chrome.com/extensions/runtime#method-getManifest)
  - [getURL](https://developer.chrome.com/extensions/runtime#method-getURL)
  - [id](https://developer.chrome.com/extensions/runtime#property-id)
  - [onConnect](https://developer.chrome.com/extensions/runtime#event-onConnect)
  - [onMessage](https://developer.chrome.com/extensions/runtime#event-onMessage)
  - [sendMessage](https://developer.chrome.com/extensions/runtime#method-sendMessage)
- [extension](https://developer.chrome.com/extensions/extension) ( [getURL](https://developer.chrome.com/extensions/extension#method-getURL) , [inIncognitoContext](https://developer.chrome.com/extensions/extension#property-inIncognitoContext) , [lastError](https://developer.chrome.com/extensions/extension#property-lastError) , [onRequest](https://developer.chrome.com/extensions/extension#event-onRequest) ,[sendRequest](https://developer.chrome.com/extensions/extension#method-sendRequest) )

## Settings

```json
  "content_scripts": [
    {
      "matches": ["http://*.nytimes.com/*"],
      "run_at": "document_idle",
      "js": ["contentScript.js"]
    }
  ],
```

##### Run_at

- `document_idle` ( **default**) - Guaranted to run after DOM is loaded so no needed to wait for window.onload
- `document_start` - after css, but before any DOM or script is run
- `document_end` - immediately after DOM is complete, but before subresources like images and frames have loaded

There is fancy matching settings and white and black lists

## Orphaned Content Scripts

When you refresh/update the background script, the content scripts on past pages will still be there running code. But, they will not have access to localStorage or be able to message

The best way to check if valid is to try to access localStorage, but can also just ensure the content script only runs code on messages or storage changes

##### Injecting Content Script into Active Tab if needed

```javascript
export async function getActiveTab() {
  const tabs = await browser.tabs.query({
    lastFocusedWindow: true,
    active: true
  });
  if (tabs.length === 0) {
    const message = "There is no active tab";
    debug(message);
    throw new Error(message);
  }

  return tabs[0];
}

export async function getValidActiveTab() {
  const activeTab = await getActiveTab();
  const tabId = activeTab.id;

  try {
    await browser.tabs.sendMessage(tabId, { type: C.test });
  } catch (_) {
    try {
      await browser.tabs.executeScript(tabId, {
        file: "build/content.js"
      });
      debug("Injected content script");
    } catch (_) {
      throw new Error(browser.runtime.lastError.message);
    }
  }

  return activeTab;
}
```

