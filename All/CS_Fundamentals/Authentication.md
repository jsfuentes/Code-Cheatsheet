# Authentication

## Json Web Tokens (JWT)

- **Compact**, could be sent in url `aaaaa.bbbbb.ccccc`
- **Self-contained**, contains everything authenticating user and crypto proof hidden by secret that it was created by your server. (Could fall out of sync with db and harder to selectively invalidate server-side)
- Usually signed by either RS256(assymetric) or HS256(symmetric)
-  Signed tokens can verify the *integrity* of the claims contained within it, while encrypted tokens *hide* those claims from other parties.

#### Parts

- **Header**
- **Payload**
- **Signature**

If you put the components together a very generic JWT looks like this:

```
aaaaa.bbbbb.ccccc
```

## Cookie Session

- Store a signed session_id/user_id in a cookie
- Store the session information server side or in database
- Cookie mechanics mean it opens up problems like CSRF(though JWT often in cookies too) and ?not as good for public APIs?

## OAuth

- Protocol to get user authentication from a 3rd party service