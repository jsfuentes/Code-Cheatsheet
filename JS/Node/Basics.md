# Basics

## Exporting
module.exports = app;

## Requiring Libs
```js
var express = require('express')
var schema = require('./schema.js')
```

## Using middleware
`app.use(bodyParser.json());`

## Adding routes
```js
var index = require('./routes/index');
app.use('/', index);
```

## Most Basic Code
```js
var express = require('express')

var app = express()

app.get('/', function (req, res) {
  res.send('Hello World!')
})

app.listen(8000, function () {
  console.log('Example app listening on port 8000!')
})
```