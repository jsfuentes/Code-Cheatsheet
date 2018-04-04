# Routing

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

## Response
- res.json()
- res.sendFile()
- res.send()
- res.redirect('/events');
- res.render('index');

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
