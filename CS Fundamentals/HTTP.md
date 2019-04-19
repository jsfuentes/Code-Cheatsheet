# HTTP

The application layer protocol of the internet, port 80 or 8080

## Methods

| HTTP method | RFC                                                          | Request has Body | Response has Body | Safe | Idempotent | Cacheable |
| ----------- | ------------------------------------------------------------ | ---------------- | ----------------- | ---- | ---------- | --------- |
| GET         | [RFC](https://en.wikipedia.org/wiki/Request_for_Comments_(identifier)) [7231](https://tools.ietf.org/html/rfc7231) | Optional         | Yes               | Yes  | Yes        | Y         |
|             |                                                              |                  |                   |      |            |           |
| POST        | [RFC](https://en.wikipedia.org/wiki/Request_for_Comments_(identifier)) [7231](https://tools.ietf.org/html/rfc7231) | Yes              | Yes               | No   | No         | Yes       |

## Overview

GET

Retrieve data of resource 

POST

accept the entity enclosed in the request as a new subordinate of the [web resource](https://en.wikipedia.org/wiki/Web_resource) identified by the URI

## Headers





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