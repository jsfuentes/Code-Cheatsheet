# Node

Node takes the JS complier in chrome browser and adds some server logic and io stuff so you can use it on the backend. So `node filename` lets you run arbitrary js logic where console.log is std.out

JS is a language

### Assert

```js
var assert = require('assert');
assert(5 > 7);
```

## Versions

```flowchart
Alice->Bob: Hello

```



- Even numbered releases are LongTerm Support(LTS); they generally receive 30 months of support once they become LTS.
- Odd numbered releases are current releases and are supported for six months.

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

##### Run for every request

```javascript
app.use(function (req, res, next) {
  console.log('Request Type:', req.method)
  next()
})
```

##### Run for specific urls

```javascript
app.get('/users/:userId/books/:bookId', function (req, res) {
  res.send(req.params) 
  // => { "userId": "34", "bookId": "8989" }
})
```

##### Types

- `app.use(...)` => for any HTTP request
- `app.get(...)` => for get request

### Globals

- `__dirname` => full from root name of the directory that the executing script resides from
- `process.env` => environment at start of runtime can use to access PATH and other env variables like `process.env.NODE_ENV`