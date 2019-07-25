# Chrome Storage

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

## Promises

From` webextension-polyfill`

```js
await browser.storage.sync.set({iframeType: "onboard"});
let storage = await browser.storage.sync.get(['iframeType', 'questions', 'lastQuestionDate']);
```