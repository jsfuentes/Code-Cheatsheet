# Routing

The app will search for the first matching route in the order you define, so define error routes last

```js
// wiki.js - Wiki route module.
var express = require('express');
var router = express.Router();
router.get('/', function (req, res) {
  res.send('Wiki home page');
})
module.exports = router;

//in app.js
var wiki = require('./wiki.js');
// ...
app.use('/wiki', wiki);
```

## Router Methods
#### Methods
- router.get
- post, put, delete, options

#### Callback
Must respond or call next

### Post

To access post data as json you need `app.use(express.json())`

To access post data you need `app.use(express.urlencoded())`

```javascript
app.post('/form', (req, res) => {
  const name = req.body.name
})
```

## Routes
Can use regex

#### Parameters
```js
app.get('/users/:userId/books/:bookId', function (req, res) {
  // Access userId via: req.params.userId
  // Access bookId via: req.params.bookId
  res.send(req.params);
})
```

## Static

```javascript
app.use(express.static('public')); 
app.use(express.static('files'));
```

Now `http://localhost:3000/images/kitten.jpg` will go to directory of `public/images/kitten.jpg`

Will search through folders in order declared returning first match

directory from where you launch your `node`process. If you run the express app from another directory, it’s safer to use the absolute path of the directory that you want to serve:

```javascript
app.use('/static', express.static(path.join(__dirname, 'public')))
```

## Error Handling

Just copied from templates

```js
const createError = require("http-errors");

//........
// catch 404 and forward to error handler
app.use(function(req, res, next) {
  next(createError(404));
});

// error handler
app.use(function(err, req, res, next) {
  // set locals, only providing error in development
  res.locals.message = err.message;
  res.locals.error = req.app.get("env") === "development" ? err : {};

  // render the error page
  res.status(err.status || 500);
  res.send("error");
});
```

