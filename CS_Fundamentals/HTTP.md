# HTTP

The application layer protocol of the internet, port 80 or 8080

## Methods

GET is supposed to be sae and idempotent

POST is to modify data

So common b/c in past browsers just supported these two and in the past browsers 

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
- Client Error `4XX`
  - 400 Bad Input
  - 401 Unauthorizaed
  - 402 Payment required. 
  - 404 Not found
  - 422 Unprocessable Entity
- Server Error `5XX`

## Headers

### Request

**Accept** request HTTP header advertises which content types, expressed as [MIME types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types), the client is able to understand.

```
Accept: <MIME_type>/<MIME_subtype>
Accept: <MIME_type>/*
Accept: */*
```

### Response

## Design

REST and all the verbs

Using id/1 is kinda a pain if you wanna do id/question in the future, but you can just make all these kinda /3241 be preceded by an id/