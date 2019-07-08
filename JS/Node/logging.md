# Logging

Could just use default `console.log` and `console.error` and then use bash redirects to a file

```
node index.js > regular.log 2> error.log
```

## Packages

- [`pino`](https://getpino.io/)
- [`winston`](https://www.npmjs.com/package/winston)
- [`roarr`](https://www.npmjs.com/package/roarr)
- `log4js`

allow for log levels, easy toggling logs on and off based on environmen

Logging frameworks will also (generally) support writing to more than just `stdout/stderr`. Winston calls these “transports” while Bunyan calls them “streams”. For example, you can configure writing to stdout, a file, and a database all at once.