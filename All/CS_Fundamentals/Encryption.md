# Encryption

Good [security resource](https://cheatsheetseries.owasp.org/)

## Password

Don't use MD5, SHA1, SHA2, SHA3, etc

Instead use something that takes longer like Blowfish with salts

### Password Reset

Tokens should:

- Expire
- Be unpredicatable
- Encrypted like credientials b/c they can basically be used a password
- Security questions?

