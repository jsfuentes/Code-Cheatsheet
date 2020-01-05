# Crypto

### Generate Random String

```js
var crypto = require("crypto");
var id = crypto.randomBytes(24).toString('hex'); //byte to hex doubles length, so this will be length 40
```

