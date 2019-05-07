# Config

With nothing special, you use Ajax 

```javascript
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = handleStateChange; // Implemented elsewhere.
xhr.open("GET", chrome.extension.getURL('/config_resources/config.json'), true);
xhr.send();
```

Or you can just use a bundler that uses imports

Or you could make a promise then await it at the start of the page, but you need ES6 for that so still a bundler