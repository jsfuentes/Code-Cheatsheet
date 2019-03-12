# Reddit API

1) https://www.reddit.com/prefs/apps - And add an app to get secret

2) Send the user to the auth url: 

```
https://www.reddit.com/api/v1/authorize?client_id=CLIENT_ID&response_type=TYPE&
state=RANDOM_STRING&redirect_uri=URI&duration=DURATION&scope=SCOPE_STRING
```

3) If authed, the user redirected to redirect_uri with code and state in query string

4) Post to the `https://www.reddit.com/api/v1/access_token`  with `grant_type=authorization_code&code=CODE&redirect_uri=URI`

