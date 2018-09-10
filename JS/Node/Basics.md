# Basics

## Exporting
module.exports = app;

Unlike js browser loading, must export not globally available

## Requiring Files

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
const express = require('express')

const app = express()

app.get('/', function (req, res) {
  res.send('Hello World!')
})

app.listen(8000, function () {
  console.log('Example app listening on port 8000!')
})
```

Can run with `node [filename]`