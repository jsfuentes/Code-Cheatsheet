# Config

With nothing special, you use Ajax 

```javascript
fetch(chrome.extension.getURL('./config.json'))
  .then(
    function(response) {
      if (response.status !== 200) {
        console.log('Looks like there was a problem. Status Code: ' +
          response.status);
        return;
      }

      // Examine the text in the response
      response.json().then(function(data) {
        console.log(data);
      });
    }
  )
  .catch(function(err) {
    console.log('Fetch Error :-S', err);
  });
```

Or you can just use a bundler that uses imports

Or you could make a promise, then use ran all your code in the callback

## Advanced

```javascript
//include this in all scripts like content, background, popup script plz
import browser from "webextension-polyfill";
import * as Sentry from "@sentry/browser";
import debugMaker from "debug"; //needed to enable in dev
const debug = debugMaker("app:scripts:dev_debug");

import C from "./constants.js";

function devSetup() {
  debugMaker.enable("app:*");
  debug("Starting debug mode");
}

function prodSetup() {
  // console.log("In production");
  Sentry.init({
    dsn: "https://96176c67c41f41c59f3cfb29a13b0b73@sentry.io/5182260",
    release: chrome.app.getDetails().version
  });
}

// if in background script
if (browser.management) {
  browser.management
    .getSelf()
    .then(pluginInfo => {
      if (pluginInfo.installType === "development") {
        devSetup();
      } else {
        prodSetup();
      }

      browser.runtime.onMessage.addListener(request => {
        if (request.type === C.is_development) {
          return new Promise(resolve =>
            resolve({ env: pluginInfo.installType })
          );
        }
      });
    })
    .catch(err => {
      console.error("Debugging error: ", err);
    });
} else {
  //hit the listener defined above to learn if in development
  browser.runtime
    .sendMessage({ type: C.is_development })
    .then(resp => {
      if (resp.env === "development") {
        devSetup();
      } else {
        prodSetup();
      }
    })
    .catch(err => {
      console.error("Debugging error: ", err);
    });
}

//Debug local storage changes
browser.storage.onChanged.addListener((changes, namespace) => {
  for (let key in changes) {
    const storageChange = changes[key];
    const oldValue = storageChange.oldValue;
    const newValue = storageChange.newValue;
    //not all in `` b/c it abbreivates objs there
    if (key === "user") {
      if (newValue) {
        //configure error scope on user change
        debug("Configured scope");
        Sentry.configureScope(scope => {
          scope.setUser({ email: newValue.email });
        });
      }

      debug(
        `${namespace} ${key} changed from`,
        oldValue ? oldValue.email : oldValue,
        "to",
        newValue ? newValue.email : newValue
      );
    } else {
      debug(`${namespace} ${key} changed from`, oldValue, "to", newValue);
    }
  }
});

browser.runtime.onMessage.addListener(msg => {
  debug("Message recieved", msg);
  // Content script debug messages will be slightly delayed
  // console.log("Message recieved", msg);
});

//only in background script
if (browser.runtime.onMessageExternal) {
  browser.runtime.onMessageExternal.addListener(msg => {
    debug("External Message recieved", msg);
    // Content script debug messages will be slightly delayed
    // console.log("Message recieved", msg);
  });
}

```

