# Packages

npm packages particularly for the server

## Default Node Packages

### fs

- Read relative to `process.cwd()`

```javascript
const fs = require("fs");

fs.readFile(filePath, (err, content) => {
	//.....
});
```

Has promise version

```js
const fs = require('fs').promises;
```



### Utils

Turn a callback style ft with (err, content) into promise returning content

```js
const util = require('util');

const read = util.promisify(fs.readFile);

const data = await read('test.txt');
```

## Extra

### Debug

Create decorated/filterable log statements

```js
const debug = require('debug')('http');

debug("booting %o", name);
```

To see http, `export DEBUG=http` environment variable with space/comma-delimited names, or `export DEBUG=*`

Can also use in browers then set `localStorage.debug = 'worker:*'`

### http-erros

```js
const createError = require('http-errors')
 
app.use(function (req, res, next) {
  if (!req.user) return next(createError(401, 'Please login to view this page.'))
  next()
})
```

### cheerio 

Fast, flexible & lean implementation of core jQuery designed specifically for the server.

```js
const cheerio = require('cheerio')
const $ = cheerio.load('<h2 class="title">Hello world</h2>')
 
$('h2.title').text('Hello there!')
$('h2').addClass('welcome')
 
$.html()
```

#### node-cron

easy cron jobs 

```js
import cron from "node-cron";

cron.schedule("* * * * *", () => {
  console.log(`this message logs every minute`);
});
```

#### node-schedule 

easy more advanced scheduler

```js
const schedule = require('node-schedule');
 
var j = schedule.scheduleJob('42 * * * *', function(){
  console.log('The answer to life, the universe, and everything!');
});
```

#### Shells 

run bash scripts

```javascript
const shell = require("shelljs");

if (shell.exec("sqlite3 database.sqlite  .dump > data_dump.sql").code !== 0) {
  shell.exit(1);
}
else{
  shell.echo("Database backup complete");
}
```

#### Nodemailer

send mail