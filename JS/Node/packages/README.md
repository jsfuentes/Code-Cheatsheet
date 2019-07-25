# Packages

npm packages particuarly for the server

## Some packages

- cheerio - Fast, flexible & lean implementation of core jQuery designed specifically for the server.

  ```js
  const cheerio = require('cheerio')
  const $ = cheerio.load('<h2 class="title">Hello world</h2>')
   
  $('h2.title').text('Hello there!')
  $('h2').addClass('welcome')
   
  $.html()
  ```

- node-cron - easy cron jobs 

```js
import cron from "node-cron";

cron.schedule("* * * * *", () => {
  console.log(`this message logs every minute`);
});
```

- node-schedule - easy more advanced scheduler

```js
const schedule = require('node-schedule');
 
var j = schedule.scheduleJob('42 * * * *', function(){
  console.log('The answer to life, the universe, and everything!');
});
```

- Shells - run bash scripts

```javascript
const shell = require("shelljs");

if (shell.exec("sqlite3 database.sqlite  .dump > data_dump.sql").code !== 0) {
  shell.exit(1);
}
else{
  shell.echo("Database backup complete");
}
```

- Nodemailer - send mail