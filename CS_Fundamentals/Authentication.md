# Authentication

## Json Web Tokens (JWT)

- **Compact**, could be sent in url `aaaaa.bbbbb.ccccc`
- **Self-contained**, contains everything about user
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

## OAuth

- Protocol to get user authentication from a 3rd party service