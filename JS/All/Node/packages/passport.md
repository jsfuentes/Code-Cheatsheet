# Passport

```
npm install passport
```

Easily integrate different logins with an authentication middleware

```js
app.post('/login', passport.authenticate('local', { successRedirect: '/',
                                                    failureRedirect: '/login' }));
```

## Google

```javascript
npm install passport-google-oauth20
```

1) Get a Google_client_id and secret by creating a project at https://console.developers.google.com/apis/dashboard and making an Oauth 2.0 client in credentials

2) 

```javascript
const passport = require('passport');
const GoogleStrategy = require('passport-google-oauth20').Strategy;

passport.use(new GoogleStrategy({
    clientID: GOOGLE_CLIENT_ID,
    clientSecret: GOOGLE_CLIENT_SECRET,
    callbackURL: "http://www.example.com/auth/google/callback"
  },
  function(accessToken, refreshToken, profile, cb) {
    User.findOrCreate({ googleId: profile.id }, function (err, user) {
      return cb(err, user);
    });
  }
));
```

