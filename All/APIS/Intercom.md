# Intercom

- Probably use segment as a source to add it

- Can turn off by default

```
npm i -D @types/intercom-web
```

```ts
export function tryUntilWorks(f: Function, name = "") {
  let tryCount = 0;

  const intervalId = setInterval(() => {
    // debug("Try until works", name);
    try {
      if (tryCount > ANALYTICS_MAX_TRIES) {
        debug(`Analytics fail - ${name}`);
        Sentry.captureMessage(`Analytics fail - ${name}`);
        clearInterval(intervalId);
        return;
      }
      f();
      clearInterval(intervalId);
    } catch (e) {
      // debug(name, e);
      //can't find variable is Safari, analytics is not defined is Chrome/Firefox
      if (
        e.message !== "analytics is not defined" &&
        e.message !== "Can't find variable: analytics" &&
        e.message !== "Cannot read properties of undefined (reading 'ready')" &&
        e.message !== "Cannot read properties of undefined (reading 'ready')" &&
        e.message !==
          'can\'t access property "ready", window.analytics is undefined' &&
        e.message !==
          "undefined is not an object (evaluating 'window.analytics.ready')"
      ) {
        debug("Unknown analytics fail error|", e.message);
        Sentry.captureException(e);
      }

      tryCount++;
      return;
    }
  }, ANALYTICS_RETRY_DELAY);
}

//INTERCOM
export function showIntercom() {
  tryUntilWorks(() => {
    window.analytics.ready(() => {
      // window.Intercom("update", { hide_default_launcher: false });
      window.Intercom("show");
      debug("Showed Intercom");
    });
  }, "Show Intercom");
}

export function hideIntercom() {
  tryUntilWorks(() => {
    window.analytics.ready(() => {
      window.Intercom("update", {
        hide_default_launcher: true,
      });
      debug("Hid Intercom");
    });
  }, "Hide Intercom");
}
```

