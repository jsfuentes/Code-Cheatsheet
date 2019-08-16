# Importing

There are packages that work just in the browser, just in react, just for gatsby, or just for node

And there are some that work for multiple like `debug` working for node and browsers

## Require

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

## Import

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

