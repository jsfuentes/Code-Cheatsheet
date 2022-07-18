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

Login with Google Through the Plugin

```js
import { getAxios, getExtendedConfig } from "../shared/utils.js";
import browser from "webextension-polyfill";

export async function resetToken(gaccess_token) {
  try {
    const url = `https://accounts.google.com/o/oauth2/revoke?token=${gaccess_token}`;
    const axios = await getAxios();
    await axios.get(url);
  } finally {
    //it fails if invalid token
    await browser.identity.removeCachedAuthToken({ token: gaccess_token });
  }
}

export default async function loginWithGoogle(interactive = true) {
  return new Promise((resolve, reject) => {
    browser.identity.getAuthToken({ interactive }, async gaccess_token => {
      if (browser.runtime.lastError) {
        return;
      }
      debug("Token", gaccess_token);
      const resp = await axios.get(`https://www.googleapis.com/oauth2/v1/userinfo?alt=json&access_token=${gaccess_token}`);
      const profile = resp.data;
      const user = {
        gid: profile.id,
        name: profile.name,
        pic: profile.picture,
        email: profile.email,
        verified_email: profile.verified_email,
        locale: profile.locale,
        status: "ready",
        gaccess_token,
        test
      };
      await browser.storage.sync.set({ user });
      resolve(user);
    });
  });
}
```

Creating oauth flow - https://developer.chrome.com/extensions/tut_oauth

On `identity.getAuthToken`  which does the whole google login popup-https://developer.chrome.com/apps/app_identity#update_manifest - 

See possible Oauth scropes - https://developers.google.com/identity/protocols/googlescopes

