# [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

Cross-Origin Resource Sharing ([CORS](https://developer.mozilla.org/en-US/docs/Glossary/CORS))

By default, requests are blocked if not same origin

**SERVER** must be configured to return the resource with the `Access-Control-Allow-Origin: *`  or the specific domain you wish to allow

All non idempotent(besides GET and some POSTS with specific meme) will be first fetched with an OPTIONS 