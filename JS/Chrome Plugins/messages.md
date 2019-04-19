# Messages

To communicate between the content script and the background script, you need to send Messages

There exists a React Store for Chrome Plugin made by Go Guardian to foster this communication

The code is the same on both sides of the payload

```javascript
chrome.runtime.sendMessage(payload); //send message

chrome.runtime.onMessage.addListener( // 
    function(request, sender, sendResponse) {
            if (request.type === "photo") {
        console.log("Photo Request: ", request);
        chrome.tabs.captureVisibleTab(sender.tab.windowId, {quality: 10},
          function(screenshotData) {
          	...
        });
    }
});
```





