# HTTP

The application layer protocol of the internet, port 80 or 8080

## Methods

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

Most common is Rest Resources with some rpc like functions calls thrown in

#### Rest

- REST, mostly about defining resources at an endpoint like `/event` that you can then do get, create, update, in an idomatic way.

- Relies heavily on HTTP defaults like caching

- Ideal is complete decoupling of client and server (HAL, JSON-API, etc)
- Large payload sizes often requiring many http calls to populate a page
- Best for most general use case with many clients, clear documentation, and focus on objects/resources

`event/1/question` to add to an id

#### GraphQL

- Instead of modeling fts or resources, you model queries. 

- Can specify the specific data you want
- Strongly typed schema sending queries
- Most Complex, but low coupling and high efficiency especially for graphs
- Best for graph-like data and weak, decoupled clients like mobile

#### RPC

- Basically everything is a function you call like `listEvents?id=1`, more common actually. gRPC is a very effiecient google implementation based on HTTP/2.

- More efficient, but more tight coupling

- Great for internal microservices sending secure messages

- Best for action-oriented and simple interactions like Slack join or leave channel. Best for efficiency with little metadata

  