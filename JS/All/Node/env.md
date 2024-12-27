# Env

See packages/dotenv

Node.js 20 adds support for .env. files

```bash
node --env-file=.env app.js
```

then in code

```js
process.env.PORT; // "3000"
```

