# Events

#### When Installed

```javascript
chrome.runtime.onInstalled.addListener(() => {
  //......
});
```

#### Bookmarks Created

```javascript
chrome.bookmarks.onCreated.addListener(function() {
  //......
});
```

#### Tab changes

[tabs.onUpdated](https://developer.chrome.com/extensions/extensions/tabs#event-onUpdated)

#### Navigation to Page

webNavigation supports filters

```javascript
 chrome.webNavigation.onCompleted.addListener(() => {
      alert("This is my favorite website!");
  }, {url: [{urlMatches : 'https://www.google.com/'}]});
```