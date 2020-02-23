# Sentry (Debug In Prod)

Add the sdk and it will automatically capture any fatal errors

```js
import * as Sentry from "@sentry/electron";

Sentry.init({
  dsn: "https://[hi]@sentry.io/2590109",
  release: "slingshow@" + process.env.npm_package_version
});
```

## Manually Logging

```js
import * as Sentry from "@sentry/electron";

try {
    aFunctionThatMightFail();
} catch (err) {
    Sentry.captureException(err);
}

Sentry.captureMessage('Something went wrong');
```

### Adding Context

Can add id, username, email, or ip_address

```js
Sentry.configureScope(function(scope) {
  scope.setUser({"email": "john.doe@example.com"});
});
```

