# Messages

To communicate between the content script and the background script, you need to send Messages

There exists a React Store for Chrome Plugin made by Go Guardian to foster this communication

The code is the same on both sides of the payload

### Send Message

```javascript
chrome.runtime.sendMessage(payload); //send message

//send message and interact with response
chrome.runtime.sendMessage({type: "gid"}, function(response) {
  var id_encrypted = CryptoJS.SHA3(response.id+secret).toString(CryptoJS.enc.Hex);
  that.setState({
    google_id: id_encrypted
  })
});
```

### Listener

```javascript
chrome.runtime.onMessage.addListener(
    function(request, sender, sendResponse) {
      if (request.type === "gid") {
        chrome.identity.getProfileUserInfo(function(userInfo){
            // console.log('Student ID: ', userInfo.id)
            sendResponse(userInfo);
        });
        return true; //must return true to sendResponse async
      }
});
```

#### Sender Info

```javascript
 let windowId = sender.tab.windowId;
```





