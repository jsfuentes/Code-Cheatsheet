# [Chrome Plugins](https://developer.chrome.com/extensions/devguide)

- Chrome.runtime is available on any webpage
- Since Manifest V3, can't use any remote code including any CDNs or packages that load code remotely

To get file from built folder,

```js
chrome.runtime.getURL("../myfile.html"); //relative path
```

Catch errors

```js
chrome.runtime.lastError.message
```

## Keep constant Chrome-ID

Add key value to the manifest.json

1. Go to https://chrome.google.com/webstore/developer/dashboard/ and click more Info to get the key
3. Add that key value to your manifest.json

