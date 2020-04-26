# HTTP

The application layer protocol of the internet, port 80 or 8080

## Methods

GET is supposed to be safe and idempotent

POST is to modify data

So common b/c in past browsers just supported these two

| HTTP method | RFC                                                          | Request has Body | Response has Body | Safe | Idempotent |
| ----------- | ------------------------------------------------------------ | ---------------- | ----------------- | ---- | ---------- |
| GET         | [RFC](https://en.wikipedia.org/wiki/Request_for_Comments_(identifier)) [7231](https://tools.ietf.org/html/rfc7231) | Optional         | Yes               | Yes  | Yes        |
| POST        | [RFC](https://en.wikipedia.org/wiki/Request_for_Comments_(identifier)) [7231](https://tools.ietf.org/html/rfc7231) | Yes              | Yes               | No   | No         |

## Status Codes

- Informational `1XX`
- Successful `2XX`
  - 200 Ok
  - 201 Created
  - 204 No Content
- Redirection `3XX`
  - 304 Client's copy of a resource is still valid
- Client Error `4XX`
  - 400 Bad Input
  - 401 Unauthorizaed
  - 402 Payment required. 
  - 403  Forbidden
  - 404 Not found
  - 422 Unprocessable Entity
- Server Error `5XX`

## Headers

### Request

##### Content-Type

```javascript
'content-type': 'multipart/form-data; boundary=...'
Content-Type: text/html; charset=UTF-8
```

`multipart/*`  requires the `boundary` parameter so server can parse payload

**Accept** request HTTP header advertises which content types, expressed as [MIME types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types), the client is able to understand.

```
Accept: <MIME_type>/<MIME_subtype>
Accept: <MIME_type>/*
Accept: */*
```

### Response

## Cookies

If you want to support **most** browsers, then don't exceed **50 cookies per domain**, and don't exceed **4093 total bytes per domain** 

Often used to store sessions, just store session/user id in a cookie with a signature

A cookie with no expiration date specified will expire when the browser is closed i.e `session` key set to true. 

Servers set cookies with`Set-Cookie` header

Browser sends cookies with `Cookie` header

Cookie properties to control domains sent to:

- `Secure`: This will ensure that cookies can only be sent to HTTPS servers.
- `Domain`: A list of hosts that a cookie can be sent to.
- `Path`: Similar to `Domain` but restricts the cookie from being sent to URLs that do not include the `Path`.

Cookies are sent with every request to the server, even those from other sites :O, this can lead to CSRF where another website tricks the user into sending a get/post request to your server with their auth. 

## Design

REST and all the verbs

Using id/1 is kinda a pain if you wanna do id/question in the future, but you can just make all these kinda /3241 be preceded by an id/