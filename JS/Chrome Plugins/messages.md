# Messages

To communicate between the content script and the background script, you need to send Messages

There exists a React Store for Chrome Plugin made by Go Guardian to foster this communication

The code is the same on both sides of the payload

## Between Background and Content

### Send Message

```javascript
chrome.runtime.sendMessage(payload); //send message

//send message and interact with response
chrome.runtime.sendMessage({type: "gid", "data": {....}}, (resp) => {
  debug(resp);
});
```

### Listener

```javascript
chrome.runtime.onMessage.addListener(
    function(request, sender, sendResponse) {
      if (request.type === "gid") {
        console.log(request.data);
        chrome.identity.getProfileUserInfo(
          (userInfo) => {
            // console.log('Student ID: ', userInfo.id)
            sendResponse(userInfo);
        	}
        );
        return true; //needed if sendResponse async
      }
});
```

#### Sender Info

```javascript
 let windowId = sender.tab.windowId;
```

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

```js
// For simple requests:
chrome.runtime.onMessageExternal.addListener(
  function(request, sender, sendResponse) {
    if (sender.id == blocklistedExtension)
      return;  // don't allow this extension access
    else if (request.getTargetData)
      sendResponse({targetData: targetData});
    else if (request.activateLasers) {
      var success = activateLasers();
      sendResponse({activateLasers: success});
    }
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

