# Essential Packages

[Common Express Middleware](<https://expressjs.com/en/resources/middleware.html>)

- body-parser: parses request bodies for POST parameters.

  - `app.use(bodyParser.json())` 
- cookie-parser: Used to parse the cookie header and populate req.cookies (essentially provides a convenient method for accessing cookie information).
- morgan: An HTTP request logger middleware for node.
- `app.use(morgan('dev'))`
  - => `GET / 200 17.199 ms - -`
- serve-favicon: Node middleware for serving a favicon (this is the icon used to represent the site inside the browser tab, bookmarks, etc.).

# Debug

Create decorated/filterable log statements

```js
const debug = require('debug')('http');

debug("booting %o", name);
```

To see http, `export DEBUG=http` environment variable with space/comma-delimited names

## fs

- Read relative to `process.cwd()`

```javascript
fs.readFile(filePath, (err, content) => {
	//.....
});
```

## Utils

Turn a callback style ft with (err, content) into promise returning content

```js
const read = util.promisify(fs.readFile);

const data = await read('test.txt');
```