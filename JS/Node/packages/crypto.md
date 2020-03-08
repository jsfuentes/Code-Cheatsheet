# Crypto

### Generate Random String

```js
var crypto = require("crypto");
var id = crypto.randomBytes(24).toString('hex'); //byte to hex doubles length, so this will be length 40
```

## Nanoid

https://github.com/ai/nanoid

```js
const nanoid = require('nanoid')
model.id = nanoid()//=> "V1StGXR8_Z5jdHi6B-myT"
nanoid(10) //=> "IRFa-VaY2b"
```

