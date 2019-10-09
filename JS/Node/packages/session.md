# Expressjs/session

Stores session in cookie

```bash
npm install express-session
```

### Initialize

```js
const session = require('express-session');

app.use(session({
    name: 'e_c',
    secret: 'super secret not secret',
    saveUninitialized: true,
    secure: false,
    resave: true,
    store: new MemoryStore({
      checkPeriod: 86400000 // prune expired entries every 24h
    })
}));
```

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

## Backing Session with Knex

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



