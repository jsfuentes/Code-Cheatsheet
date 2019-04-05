# Node

Node takes the JS complier in chrome browser and adds some server logic and io stuff so you can use it on the backend. So `node filename` lets you run arbitrary js logic where console.log is std.out

JS is a language

### Assert

```js
var assert = require('assert');
assert(5 > 7);
```

# Express

### Most Basic Code

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

### Overview

Middleware have access to request object (req), response object (res), and the next middleware ft(next). If you don't respond with res, call `next()`