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

## Oauth

Creating oauth flow - https://developer.chrome.com/extensions/tut_oauth

On `identity.getAuthToken`  which does the whole google login popup-https://developer.chrome.com/apps/app_identity#update_manifest - 

See possible Oauth scropes - https://developers.google.com/identity/protocols/googlescopes

