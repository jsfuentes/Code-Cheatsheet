# [Commander](https://www.npmjs.com/package/commander)

Lets you define command line interfaces

```
yarn add commander
```

## Usage

command.js

```js
const { Command } = require('commander');
const program = new Command();
program
  .command("join")
  .arguments("<event>")
  .description("Make bots join an event.")
  .option('-d, --debug', 'output extra debugging')
  .option("-n, --number <count>", "Number of bots to summon", 3)
  .option(
    "--host <host>",
    "Which slingshow instance to point to.",
    "localhost:4000"
  )
  .action(async (event, options) => {
    return join(event, { number: +options.number, host: options.host });
  });

program.parse(process.argv);
```

in bash

```bash
node command.js join -n 5 <event_id>
```

