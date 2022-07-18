# Http-errors

```js
const createError = require('http-errors')
 
app.use(function (req, res, next) {
  if (!req.user) return next(createError(401, 'Please login to view this page.'))
  next()
})

```

### Possible Constructors

```js
const err = new createError.NotFound("Error message here");//constructors for all HTTP errors
```

#### List of all constructors

| Status Code | Constructor Name              |
| :---------- | :---------------------------- |
| 400         | BadRequest                    |
| 401         | Unauthorized                  |
| 402         | PaymentRequired               |
| 403         | Forbidden                     |
| 404         | NotFound                      |
| 405         | MethodNotAllowed              |
| 406         | NotAcceptable                 |
| 407         | ProxyAuthenticationRequired   |
| 408         | RequestTimeout                |
| 409         | Conflict                      |
| 410         | Gone                          |
| 411         | LengthRequired                |
| 412         | PreconditionFailed            |
| 413         | PayloadTooLarge               |
| 414         | URITooLong                    |
| 415         | UnsupportedMediaType          |
| 416         | RangeNotSatisfiable           |
| 417         | ExpectationFailed             |
| 418         | ImATeapot                     |
| 421         | MisdirectedRequest            |
| 422         | UnprocessableEntity           |
| 423         | Locked                        |
| 424         | FailedDependency              |
| 425         | UnorderedCollection           |
| 426         | UpgradeRequired               |
| 428         | PreconditionRequired          |
| 429         | TooManyRequests               |
| 431         | RequestHeaderFieldsTooLarge   |
| 451         | UnavailableForLegalReasons    |
| 500         | InternalServerError           |
| 501         | NotImplemented                |
| 502         | BadGateway                    |
| 503         | ServiceUnavailable            |
| 504         | GatewayTimeout                |
| 505         | HTTPVersionNotSupported       |
| 506         | VariantAlsoNegotiates         |
| 507         | InsufficientStorage           |
| 508         | LoopDetected                  |
| 509         | BandwidthLimitExceeded        |
| 510         | NotExtended                   |
| 511         | NetworkAuthenticationRequired |