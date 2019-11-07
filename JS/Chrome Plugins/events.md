# Events

### One time Intialization

```
  chrome.runtime.onInstalled.addListener(function() {
```



```
  // This will run when a bookmark is created.
  chrome.bookmarks.onCreated.addListener(function() {
    // do something
  });
```

## Tab changes

[tabs.onUpdated](https://developer.chrome.com/extensions/extensions/tabs#event-onUpdated)

webNavigation supports filters

```
  chrome.webNavigation.onCompleted.addListener(function() {
      alert("This is my favorite website!");
  }, {url: [{urlMatches : 'https://www.google.com/'}]});
```