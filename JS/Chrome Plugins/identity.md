# To Get Identity

And get permissions for `identity` and `identity.email`

```javascript
chrome.runtime.onMessage.addListener(
    function(request, sender, sendResponse) {
      if (request.type === "gid") {
        chrome.identity.getProfileUserInfo(function(userInfo){
            console.log('Student ID: ', userInfo.id);
            sendResponse(userInfo);
        });
        return true;
      }
});
```

