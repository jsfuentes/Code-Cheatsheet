# PassLib

- Supports many hashing types with simple interface

`pip install passlib`

```python
from passlib.hash import pbkdf2_sha256

# generate new salt, and hash a password
hash = pbkdf2_sha256.hash("toomanysecrets")
#hash '$pbkdf2-sha256$29000$N2YMIWQsBWBMae09x1jrPQ$1t8iyB2A.WF/Z5JZv.lfCIhXXN33N23OSgQYThBYRfk'

pbkdf2_sha256.verify("toomanysecrets", hash)
#True
pbkdf2_sha256.verify("joshua", hash)
#False
```

## Alternatives

- Werkzeug.security
- Bcrypt
