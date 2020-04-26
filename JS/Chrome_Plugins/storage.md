# Chrome Storage

## Promises

From ` webextension-polyfill`

```js
await browser.storage.sync.set({iframeType: "onboard"});
let storage = await browser.storage.sync.get(['iframeType', 'questions', 'lastQuestionDate']);
const { iframeType } = storage;
```

To check out limits: Go to background script, type `chrome.storage.sync.` then let browser autocomplete

## Chrome

### Local

their chrome local

```javascript
chrome.storage.local.set({key: value}, function() {
  console.log('Value is set to ' + value);
});

chrome.storage.local.get(['key'], function(result) {
  console.log('Value currently is ' + result.key);
});   
```

### Global

Syncs to google id, their sync must be enabled if not is equivalent to local storage saves

```javascript
chrome.storage.sync.set({key: value}, function() {
  console.log('Value is set to ' + value);
});

chrome.storage.sync.get(['key'], function(result) {
  console.log('Value currently is ' + result.key);
});
```

## Other

```js
chrome.storage.sync.clear();//to empty storage
```

##### Detect Changes

```js
browser.storage.onChanged.addListener((changes, namespace) => {
  for (let key in changes) {
    const storageChange = changes[key];
    const oldValue = storageChange.oldValue;
    const newValue = storageChange.newValue;
    //not all in `` b/c it abbreivates objs there
    debug(`${namespace} ${key} changed from`, oldValue, "to", newValue);
  }
});
```

