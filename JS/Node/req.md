# Req

Express v4 requires extra middle ware to handle POST requests

`app.use(bodyParser.json());`

Express in 4.16 again has `express.json()`

## Access

```js
req.query //query parameters
req.body //post body
req.params //url variables like /user/:userid
```

### Advanced

#### Get Ip Address

```js
const ip =
      req.headers["x-forwarded-for"] ||
      req.connection.remoteAddress ||
      req.socket.remoteAddress ||
      (req.connection.socket ? req.connection.socket.remoteAddress : null);
```

