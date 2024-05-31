# [Service Workers](https://developer.chrome.com/docs/extensions/develop/concepts/service-workers/lifecycle#persist-data)

- Terminate when not in use
  - need to persist application states
    - Use [IndexedDB](https://developer.mozilla.org/docs/Web/API/IndexedDB_API) and [Cache Storage](https://developer.mozilla.org/docs/Web/API/CacheStorage) APIs
      - [Local Storage](https://developer.mozilla.org/docs/Web/API/Window/localStorage) and [Session Storage](https://developer.mozilla.org/docs/Web/API/Window/sessionStorage) are only avilable through an [offscreen document](https://developer.chrome.com/docs/extensions/reference/offscreen).
  - need to use alarms 
  - allow start, run, and terminate repeatedly
  
- Listen to events like typing in url and stuff
  - Don't register async, it might not work

- Communicate with content script to activate page actions and has access to chrome apis
- Chrome terminates a service worker:
  - After 30 seconds of inactivity. Receiving an event or calling an extension API resets this timer.
  - When a single request, such as an event or API call, takes longer than 5 minutes to process.
  - When a [`fetch()`](https://developer.mozilla.org/docs/Web/API/fetch) response takes more than 30 seconds to arrive.

## Transform Timers into Alarms[#](https://developer.chrome.com/extensions/background_migration#timers)

DOM-based timers, such as `window.setTimeout()` or `window.setInterval()`, are not honored

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

## [Just Keep Service Worker Online](https://developer.chrome.com/docs/extensions/develop/migrate/to-service-workers#keep_a_service_worker_alive_until_a_long-running_operation_is_finished)

- consider bad practice, butttt also in Chrome docs so...
- [just run it forever, extra Chrome bad practice](https://developer.chrome.com/docs/extensions/develop/migrate/to-service-workers#keep_a_service_worker_alive_continuously)

```js
async function waitUntil(promise) = {
  const keepAlive = setInterval(chrome.runtime.getPlatformInfo, 25 * 1000);
  try {
    await promise;
  } finally {
    clearInterval(keepAlive);
  }
}

waitUntil(someExpensiveCalculation());
```