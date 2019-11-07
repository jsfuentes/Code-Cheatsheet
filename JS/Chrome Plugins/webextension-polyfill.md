# [WebExtension-Polyfill](https://github.com/mozilla/webextension-polyfill )

```bash
npm install --save-dev webextension-polyfill
```



```js
import browser from "webextension-polyfill";

browser.storage.sync.get(['isOnboarded', 'iframeType', 'nextMessage', 'messageHistory']).then(
  (storage) => {
    //...
  });

browser.runtime.onMessage.addListener((msg, sender) => {
  if(msg.type === "closeIframe") {
    // console.log("Closing Iframe");
    removeIframe();
  }
});
```

