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
