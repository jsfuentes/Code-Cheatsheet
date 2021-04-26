# Sentry (Debug In Prod)

Add the sdk and it will automatically capture any fatal errors

[As of May 2020](https://forum.sentry.io/t/react-install-fails-with-projectid-error/9620/7),  must wait about an hour after project is created to use

## Javascript

All javascript libs have the same API:

@sentry/electron | @sentry/browser | @sentry/node

```js
import * as Sentry from "@sentry/browser";

if(process.env.NODE_ENV === "production") {
  Sentry.init({dsn: "https://[hi]@sentry.io/2590109"});
}
```

If Sentry.init isn't called, all other Sentry functions are noops

#### Manually Logging

```js
import * as Sentry from "@sentry/electron";

try {
    aFunctionThatMightFail();
} catch (err) {
    Sentry.captureException(err);
}

Sentry.captureMessage('Something went wrong');
```

#### Adding Context in General

Can add id, username, email, or ip_address

*Don't add extra objects of arbitary size as they [will be rejected](https://github.com/getsentry/sentry-javascript/issues/339) if over 100KB*

```js
Sentry.configureScope((scope) => {
  scope.setUser({"email": "john.doe@example.com"});
}); //will be for all messages

Sentry.setContext("profile", { name: "Jorge", time: 1 });
```

#### Adding Context for a Message

```elixir
Sentry.captureException(new Error("something went wrong"), {
  extra: {
    section: "articles",
  },
});
```

#### Creating Error Popup

```js
  Sentry.init({
    dsn: "https://adsfasdfvcxzdsaf@sentry.io/2898629",
    beforeSend(event, hint) {
      // Check if it is an exception, and if so, show the report dialog
      if (event.exception) {
        Sentry.showReportDialog({ eventId: event.event_id });
      }
      return event;
    }
  });
```

## Server-Side

#### Node Specific

```js
const express = require('express');
const app = express();
const Sentry = require('@sentry/node');

Sentry.init({ dsn: 'https://jdfasklfjdajfdiopiuasdfop@sentry.io/5182247' });

// The request handler must be the first middleware on the app
app.use(Sentry.Handlers.requestHandler());

// All controllers should live here
app.get('/', function rootHandler(req, res) {
  res.end('Hello world!');
});

// The error handler must be before any other error middleware and after all controllers, by default only captures 500
app.use(Sentry.Handlers.errorHandler());

// Optional fallthrough error handler
app.use(function onError(err, req, res, next) {
  // The error id is attached to `res.sentry` to be returned
  // and optionally displayed to the user for support.
  res.statusCode = 500;
  res.end(res.sentry + "\n");
});

app.listen(3000);
```

To capture all errors instead of just over 500

```js
app.use(
  Sentry.Handlers.errorHandler({
    shouldHandleError(err) {
      return true; //by default only captures 500, but lets capture all errors
    }
  })
); //must be first error handler and after all controllers
```

