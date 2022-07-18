# [Chrome Plugins](https://developer.chrome.com/extensions/devguide)

Chrome.runtime is available on any webpage

Use `browser` from [webextension-polyfill](](https://github.com/mozilla/webextension-polyfill )) for promise-based, cross browser support

```bash
npm install --save-dev webextension-polyfill
```

To get file from built folder,

```js
browser.runtime.getURL("../myfile.html"); //relative path
```

Catch errors

```js
browser.runtime.lastError.message
```

## Keep constant Chrome-ID

Add key value to the manifest.json

1. Go to https://chrome.google.com/webstore/developer/dashboard/ and click more Info to get the key
3. Add that key value to your manifest.json

