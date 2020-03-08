# Expressjs/session

Stores session in cookie

```bash
npm install express-session
```

### Initialize

The default MemoryStore is NOT DESIGNED FOR PRODUCTION pleases back it with [compatible session stores](https://www.npmjs.com/package/express-session#compatible-session-stores).

```js
const session = require('express-session');

app.use(session({
    name: 'e_c',
    secret: 'super secret not secret',
    saveUninitialized: true,
    secure: false, //only https
    resave: true,
    maxAge: 7 * 24 * 60 * 60 * 1000, // one week
}));
```

Need maxAge or expires or the session will expire immediately

### Usage

```js
// Access the session as req.session
app.get('/', function(req, res, next) {
  if (req.session.views) {
    req.session.views++
    res.setHeader('Content-Type', 'text/html')
    res.write('<p>views: ' + req.session.views + '</p>')
    res.write('<p>expires in: ' + (req.session.cookie.maxAge / 1000) + 's</p>')
    res.end()
  } else {
    req.session.views = 1
    res.end('welcome to the session demo. refresh!')
  }
})
```

## Backing Sessions

##### Knex

```bash
npm install connect-session-knex
```

```js
const session = require('express-session')
const KnexSessionStore = require('connect-session-knex')(session);

//.....

app.use(session({
  name: 'ecstatic_cookie',
  secret: 'ecstatic secret',
  saveUninitialized: true,
  secure: false,
  resave: true,
  store: new KnexSessionStore({
    knex: AppUtils.getKnex(),
    tablename: 'sessions' //default
  })
}));
```

##### Mongo

```bash
npm install connect-mongo
```

```js
const session = require('express-session')
const MongoStore = require('connect-mongo')(session);

const mongoose = require('mongoose');

// Basic usage
mongoose.connect(connectionOptions);

app.use(session({
    store: new MongoStore({ mongooseConnection: mongoose.connection })
}));
```



