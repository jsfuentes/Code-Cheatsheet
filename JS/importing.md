# Importing

There are packages that work just in the browser, just in react, just for gatsby, or just for node

And there are some that work for multiple like `debug` working for node and browsers

## Module Types

ECMA Modules(import) webpack/babel often, async loaded

- Absolute paths are currently not supported
- Relative paths are resolved relative to current module path
- automatically in [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode/Transitioning_to_strict_mode), (mistakes into errors, simplifying/easier JS, anticpate future ECMA evolution)

CommonJS(require) node default, sync loaded

- Have access to `__filename` and `__dirname`

`.mjs` extension in node: 

- Uses ECMA, but can cause problems if you use CommonJS modules too
- Can import commonjs files, but .js cant use .mjs

Use std/esm to use .mjs in .jsj

main.js

```js
require = require("@std/esm")(module);
module.exports = require("./hi-web.mjs").default;
```

Access Node builtin modules

```js
import * as path from 'path';
```

### Require (CommonJS)

Exporting

```js
//module.exports = router;
module.exports = {
  insertOne,
  queryByUniqueId
};
```

Importing

```js
const conf = require("config");
const Phrase = require('../dao/phrase_dao');
```

###Import (EMCAScript)

Exporting

```js
//export let months = ['Jan', 'Feb', 'Mar','Apr', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
export const MODULES_BECAME_STANDARD_YEAR = 2015;
export default class User { // just add "default"
  constructor(name) {
    this.name = name;
  }
}
```

Importing

```js
import User from './user.js'; // not {User}, just User
new User('John');

import {sayHi, sayBye} from './say.js';
import * as say from './say.js';
```

Exporting Imports

```js
//export imports
import d, {obj} from '...';
export {obj, d};
export {obj as name1, d as name2};
//re-export all named imports
export * from '...';
export * as name1 from '...';
//re-export some named imports
export {a, b as name1} from '...';
//re-export default import as default export
export {default} from '...';
//re-export default import as named export
export {default as name1} from '...';
```

