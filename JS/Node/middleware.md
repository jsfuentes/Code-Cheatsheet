# Middleware

Can add as much middleware as you want to a route

```js
router.post('/moderator', [Auth.adminOfPostedId, Auth.canInvite], postModerator);
```

## Example

```js
function logged_in(req, res, next) {
  if (req.session.payload === undefined) {
    console.error("Logged_in failed to find payload");
    res.status(401)
      .json({
        status: 'failed',
        message: 'Cannot authorize the user'
      });
  }
  
  debug(`Session active for ${req.session.payload.email}`);
  next(); //call next to continue to next middleware/handler ft
}
```

### Next

`next('route')` will go to next route handler that matches, if you pass anything else into `next()` it will be considered an error