# Importing Files

```js
const fs = require('fs-extra');
```

Require avaliable everywhere

Runs the file 

## Where It Looks

Looks in core modules, then/or all paths specified by module.paths in order which is basically potentially every node_modules folder from curfolder to root

Looks for .js then .json then .node

.js in string is optional

## Folders

If don't want to just look in `node_modules` can use paths

```js
const config = require('./config');
```

Works whether a config folder with an `index.js` or config.js in the current folder 

To change main folder, can add package.json to config folder with `"main": "start.js"` and it looks at start.js

## What does require return?

Recall module is something defined for each file

require returns the `module.exports` object

So in config.js

```js
function myFunction() {
    console.log("HEYYYYY");
}

module.exports = myFunction;
```

Then in other file

```js
const config = require('./config')

config();
```

## Circular?

Returns partially loaded module.exports so it can finish

## Can I only execute code if I run this file?

Yes!

```js
if (require.main === module) {
  // The file is being executed directly (not with require)
}
```

#### how to get args though?

```js
process.argv[2], process.argv[3]
```

process.argv[1] is the filename