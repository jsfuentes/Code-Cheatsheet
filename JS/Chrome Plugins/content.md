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