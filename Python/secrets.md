# Secrets

Python 3.6 and up, default

used for generating cryptographically strong random numbers suitable for managing data such as passwords, account authentication, security tokens, and related secrets.

```python
import secrets
```

```python
>> secrets.token_hex(nbytes=16)
'17adbcf543e851aa9216acc9d7206b96'

>>> secrets.token_urlsafe(16)
'X7NYIolv893DXLunTzeTIQ'

>>> secrets.token_bytes(128 // 8)
b'\x0b\xdcA\xc0.\x0e\x87\x9b`\x93\\Ev\x1a|u'
```

