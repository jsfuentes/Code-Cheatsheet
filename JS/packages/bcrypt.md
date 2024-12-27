# Bcrypt

Cryptography/hashing lib, @node-rs/argon2 might be better

```bash
npm install bcrypt
```

## Basics

```javascript
const bcrypt = require('bcrypt');
const saltRounds = 10;
const myPlaintextPassword = 's0/\/\P4$$w0rD';
const someOtherPlaintextPassword = 'not_bacon';

//Hash Password
bcrypt.hash(myPlaintextPassword, saltRounds).then(function(hash) {
    // Store hash in your password DB.
});

// Load hash from your password DB.
bcrypt.compare(myPlaintextPassword, hash).then(function(res) {
    // res == true
});
bcrypt.compare(someOtherPlaintextPassword, hash).then(function(res) {
    // res == false
});
```