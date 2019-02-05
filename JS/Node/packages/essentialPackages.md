# Essential Packages
- body-parser: This parses the body portion of an incoming HTTP request and makes it easier to extract different parts of the contained information. For example, you can use this to read POST parameters.
- cookie-parser: Used to parse the cookie header and populate req.cookies (essentially provides a convenient method for accessing cookie information).
- debug: A tiny node debugging utility modelled after node core's debugging technique.
- morgan: An HTTP request logger middleware for node.
- serve-favicon: Node middleware for serving a favicon (this is the icon used to represent the site inside the browser tab, bookmarks, etc.).

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