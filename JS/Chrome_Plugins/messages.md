# [Messages](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/runtime/onMessage)

To communicate between the content script and the background script, you need to send Messages(or use local storage)

There exists a React Store for Chrome Plugin made by Go Guardian to foster this communication

## Between Background and Content

### Send Message

##### Content

```javascript
browser.runtime.sendMessage(payload); //send message

//send message and interact with response
chrome.runtime.sendMessage({type: "gid", "data": {....}}, (resp) => {
  debug(resp);
});
```

##### Background

Same except specify tab id and tabs sendMessage

```js
browser.tabs
  .query({ active: true, currentWindow: true })
  .then(tabs => browser.tabs.sendMessage(tabs[0].id, { type: C.toast }))
  .then(resp => debug("Got response", resp));
```

### Listener

```js
browser.runtime.onMessage.addListener(request => {
  if (request.type === C.is_development) {
    return new Promise(resolve => resolve({ e: "d"}));
  }
});
```

**Return a promise instead of sendResponse for new W3C specSender Info**

```javascript
let windowId = sender.tab.windowId; //windowId is instance of chrome, so multiple tabs in the same window have the same windowId
let tabId = sender.tab.id;
```

##### Gotchas

- Do not add an async listener `browser.runtime.addListener(async (req) => ....)` as it will consume all the messages blocking other listeners, instead use promises inside ft

## Message Passing Between Extensions

Lets you make a "public api" that other chrome extensions can use

Similar interface to regular Messages except need chrome id which you can find [here](https://stackoverflow.com/questions/8946325/chrome-extension-id-how-to-find-it)

#### Send Message

```js
// The ID of the extension we want to talk to.
var laserExtensionId = "abcdefghijklmnoabcdefhijklmnoabc";

// Make a simple request:
chrome.runtime.sendMessage(laserExtensionId, {getTargetData: true},
  function(response) {
    if (targetInRange(response.targetData))
      chrome.runtime.sendMessage(laserExtensionId, {activateLasers: true});
  });
```

#### Listener

Only in background script

```js
browser.runtime.onMessage.addListener(msg => {
  if (msg == "get-ids") {
    return browser.storage.sync.get("idPattern").then(({idPattern}) => {
      return Array.from(document.querySelectorAll(idPattern),
                        elem => elem.textContent);
    });
  }
});
```

## From Webpages

Can't do ports, can do messages

Must add to manifest.json

```json
"externally_connectable": {
  "matches": ["*://*.slingshow.com/*", "http://localhost:3000/*"]
},
```

webpage

```js
if (chrome) {
  // Make a simple request:
  debug("CE", conf.extension_id);
  chrome.runtime.sendMessage(conf.extension_id, { x: 1 }, response => {
    debug("M RESPONSE", response);
  });
}
```

Any script in extension

```js
//returning promise is now sendResponse, so async function means responses with anything returned
browser.runtime.onMessageExternal.addListener(async (msg, sender) => {
  debug("External message recieved", msg, sender);
  debug("From sender", sender.url);
  return { x: 1 };
});
```

### Long lived Connections

Background

```js
var port = chrome.runtime.connect({name: "knockknock"});
port.postMessage({joke: "Knock knock"});
port.onMessage.addListener(function(msg) {
  if (msg.question == "Who's there?")
    port.postMessage({answer: "Madame"});
  else if (msg.question == "Madame who?")
    port.postMessage({answer: "Madame... Bovary"});
});
```

content

```js
chrome.runtime.onConnect.addListener(function(port) {
  console.assert(port.name == "knockknock");
  port.onMessage.addListener(function(msg) {
    if (msg.joke == "Knock knock")
      port.postMessage({question: "Who's there?"});
    else if (msg.answer == "Madame")
      port.postMessage({question: "Madame who?"});
    else if (msg.answer == "Madame... Bovary")
      port.postMessage({question: "I don't get it."});
  });
});
```
