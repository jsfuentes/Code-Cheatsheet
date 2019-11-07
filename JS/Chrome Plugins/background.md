# Background Scripts

Always running

Listen to events like typing in url and stuff 

Communicate with content script to activate page actions and has access to chrome apis

Must look at chrome extensions for the background script stuff

## Transform Timers into Alarms[#](https://developer.chrome.com/extensions/background_migration#timers)

DOM-based timers, such as `window.setTimeout()` or `window.setInterval()`, are not honored in non-persistent background scripts if they trigger when the event page is dormant.

```js
  let timeout = 1000 * 60 * 3;  // 3 minutes in milliseconds
  window.setTimeout(function() {
    alert('Hello, world!');
  }, timeout);
```

Instead, use the [alarms API](https://developer.chrome.com/extensions/alarms).

```js
  chrome.alarms.create({delayInMinutes: 3.0})
```

Then add a listener.

```js
  chrome.alarms.onAlarm.addListener(function() {
    alert("Hello, world!")
  });
```