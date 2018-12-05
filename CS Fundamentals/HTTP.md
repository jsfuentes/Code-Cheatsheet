# HTTP

The application layer protocol of the internet, port 80 or 8080

## Methods

| HTTP method | RFC                                                          | Request has Body | Response has Body | Safe | Idempotent | Cacheable |
| ----------- | ------------------------------------------------------------ | ---------------- | ----------------- | ---- | ---------- | --------- |
| GET         | [RFC](https://en.wikipedia.org/wiki/Request_for_Comments_(identifier)) [7231](https://tools.ietf.org/html/rfc7231) | Optional         | Yes               | Yes  | Yes        | Yes       |
| HEAD        | [RFC](https://en.wikipedia.org/wiki/Request_for_Comments_(identifier)) [7231](https://tools.ietf.org/html/rfc7231) | No               | No                | Yes  | Yes        | Yes       |
| POST        | [RFC](https://en.wikipedia.org/wiki/Request_for_Comments_(identifier)) [7231](https://tools.ietf.org/html/rfc7231) | Yes              | Yes               | No   | No         | Yes       |
| PUT         | [RFC](https://en.wikipedia.org/wiki/Request_for_Comments_(identifier)) [7231](https://tools.ietf.org/html/rfc7231) | Yes              | Yes               | No   | Yes        | No        |
| DELETE      | [RFC](https://en.wikipedia.org/wiki/Request_for_Comments_(identifier)) [7231](https://tools.ietf.org/html/rfc7231) | No               | Yes               | No   | Yes        | No        |
| CONNECT     | [RFC](https://en.wikipedia.org/wiki/Request_for_Comments_(identifier)) [7231](https://tools.ietf.org/html/rfc7231) | Yes              | Yes               | No   | No         | No        |
| OPTIONS     | [RFC](https://en.wikipedia.org/wiki/Request_for_Comments_(identifier)) [7231](https://tools.ietf.org/html/rfc7231) | Optional         | Yes               | Yes  | Yes        | No        |
| TRACE       | [RFC](https://en.wikipedia.org/wiki/Request_for_Comments_(identifier)) [7231](https://tools.ietf.org/html/rfc7231) | No               | Yes               | Yes  | Yes        | No        |
| PATCH       | [RFC](https://en.wikipedia.org/wiki/Request_for_Comments_(identifier)) [5789](https://tools.ietf.org/html/rfc5789) | Yes              | Yes               | No   | No         | No        |

## Overview

#### GET

Retrieve data of resource 

HEAD

response identical to GET, but without the response body

POST

accept the entity enclosed in the request as a new subordinate of the [web resource](https://en.wikipedia.org/wiki/Web_resource) identified by the URI

PUT

requests that the enclosed entity be stored under the supplied [URI](https://en.wikipedia.org/wiki/URI). Create or update resource

DELETE

delete resource

TRACE

echoes received request to check intermediate servers

OPTIONS

returns accepted HTTP methods. Check functionality by requesting '*' instead of a specific resource.

CONNECT

converts the request connection to a transparent [TCP/IP tunnel](https://en.wikipedia.org/wiki/Tunneling_protocol), usually to facilitate [SSL](https://en.wikipedia.org/wiki/Transport_Layer_Security)-encrypted communication (HTTPS) through an unencrypted [HTTP proxy](https://en.wikipedia.org/wiki/HTTP_proxy).[[21\]](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#cite_note-21)[[22\]](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#cite_note-22) See [HTTP CONNECT method](https://en.wikipedia.org/wiki/HTTP_tunnel#HTTP_CONNECT_method).

PATCH

partial modifications to a resource

## Status Codes

- Informational `1XX`
- Successful `2XX`
- Redirection `3XX`
- Client Error `4XX`
- Server Error `5XX`