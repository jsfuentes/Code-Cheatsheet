# Middleware

Can add as much middleware as you want to a route

```js
router.post('/moderator', [Auth.adminOfPostedId, Auth.canInvite], postModerator);
```

## Example

middleware/auth.js

```js
const createError = require("http-errors");
const debug = require("debug")("app:middleware:auth");

module.exports = {
  logged_in
};

function logged_in(req, res, next) {
  if (req.session.uid === undefined) {
    throw createError().Unauthorized("Need to be logged in"); //handled by error handler
  } else {
    // debug(`Session active for ${req.session.uid}`);
    next();
  }
}
```

### Next

`next('route')` will go to next route handler that matches, if you pass anything else into `next()` it will be considered an error