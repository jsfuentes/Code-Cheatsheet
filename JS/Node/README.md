# Node

Node takes the JS complier in chrome browser and adds some server logic and io stuff so you can use it on the backend. So `node filename` lets you run arbitrary js logic where console.log is std.out

JS is a language

### Assert

```js
var assert = require('assert');
assert(5 > 7);
```

## Using middleware

Express v4 requies extra middle ware to handle POST requests

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

# Package-lock.json

You SHOULD commit your package-lock to source control

Package-lock.json ensures the version of modules used is the same

i.e npm install express would change with updates over time, but not anymore

