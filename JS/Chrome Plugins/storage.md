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

##### Detect Changes

```js
function logStorageChange(changes, area) {
  console.log("Change in storage area: " + area);
 
  var changedItems = Object.keys(changes);
 
  for (var item of changedItems) {
    console.log(item + " has changed:");
    console.log("Old value: ");
    console.log(changes[item].oldValue);
    console.log("New value: ");
    console.log(changes[item].newValue);
  }
}

browser.storage.onChanged.addListener(logStorageChange);
```

## Promises

From` webextension-polyfill`

```js
await browser.storage.sync.set({iframeType: "onboard"});
let storage = await browser.storage.sync.get(['iframeType', 'questions', 'lastQuestionDate']);
```