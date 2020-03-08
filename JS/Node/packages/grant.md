# Grant

Authentication middleware for koa, hapi, and express

## Express

```bash
npm install grant-express
```

### Server

1) Add this code with the right key and secret

```javascript
const express = require('express')
const session = require('express-session')
const grant = require('grant-express')

const app = express()
// REQUIRED: any session store - see /examples/express-session-stores
app.use(session({secret: 'hi'}))
// mount grant
app.use(grant({
  "defaults": {
    "protocol": "http",
    "host": "localhost:3000",
    "transport": "session", //querystring | session
    "state": true
  },
  "google": {
    "key": "...",
    "secret": "...",
    "scope": ["openid", "profile", "email"],
    "nonce": true,
    "custom_params": {"access_type": "offline"},
    "callback": "/hello" 
  }
}))
```

2) Set the redirect url for the oauth to `[protocol]://[host]/connect/[provider]/callback`

3) Login by navigating user to `/connect/:provider`

4) Will send the user to the defaults + callback *Can just define the full url callback*

5) The data will wither be in `req.session.grant` or `req.query` depending on the transport selected

```javascript
  if (!req.session.grant || !req.session.grant.response) {
    console.error(`Login success failed, grant: ${req.session.grant}`);
    res.redirect("/api/user/login/start");
    return;
  }
  const { access_token, refresh_token } = req.session.grant.response;

```

