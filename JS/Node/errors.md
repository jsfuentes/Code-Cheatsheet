# [Errors in Express](https://expressjs.com/en/guide/error-handling.html)

## Sync

Sync errors will just go to error handler(see below)

## Async

Crash the server:

```js
app.get("/", async (req, res) => {
  throw new Error("non async");
}
```

Send to Error Handler:

```js
app.get("/", async (req, res) => {
  next(new Error("non async"));
}
```

Passing anything to `next`(expect the string 'route') will pass to 4 arg error middleware

### Async Solutions

Async Wrapper

```js
app.get('*', wrapAsync(async (req, res) => {
  await new Promise(resolve => setTimeout(() => resolve(), 50));
  // Async error!
  throw new Error('woops');
}));

app.use(function(error, req, res, next) {
  // Gets called because of `wrapAsync()`
  res.json({ message: error.message });
});

function wrapAsync(fn) {
  return function(req, res, next) {
    // Make sure to .catch() any errors and pass them along to the `next()` middleware in the chain, in this case the error handler.
    fn(req, res, next).catch(next);
  };
}
```

Try-catch

```js
app.get('/', function (req, res, next) {
  setTimeout(function () {
    try {
      throw new Error('BROKEN')
    } catch (err) {
      next(err)
    }
  }, 100)
})
```

Promises

```js
app.get('/', function (req, res, next) {
  Promise.resolve().then(function () {
    throw new Error('BROKEN')
  }).catch(next) // Errors will be passed to Express.
})
```

## Error Handler

If any route throws an error, it will go to first error handler which has specifically 4 args:

```js
app.use(function(error, req, res, next) {
  res.json({ message: error.message });
});
```

- Can check type of error and respond with proper HTTP status
- Can define multiple error handlers and chain with next
- define last
- Should either call next or respond, final call will be to default error handler

```js
const { AssertionError } = require('assert');
const { MongoError } = require('mongodb');

app.use(function handleAssertionError(error, req, res, next) {
  if (error instanceof AssertionError) {
    return res.status(400).json({
      type: 'AssertionError',
      message: error.message
    });
  }
  next(error);
});

app.use(function handleDatabaseError(error, req, res, next) {
  if (error instanceof MongoError) {
    return res.status(503).json({
      type: 'MongoError',
      message: error.message
    });
  }
  next(error);
});
```

Catch all

```js
function errorHandler (err, req, res, next) {
  res.status(500)
  res.render('error', { error: err })
}

app.use(errorHandler);
```

 ##### Edge Case

If streaming resp and you get an error, default error handler properly closes the connection and fails the request. So you should delegate to it, if headers have already been sent to the client:

```javascript
function errorHandler (err, req, res, next) {
  if (res.headersSent) {
    return next(err)
  }
  res.status(500)
  res.render('error', { error: err })
}
```