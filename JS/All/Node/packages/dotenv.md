# Dotenv

Load .env files into your process.env

```bash
npm i dotenv
```

## Usage

As early as possible, 

```js
require('dotenv').config()
```

or

```js
import 'dotenv/config'
```

That's it. `process.env` now has the keys and values you defined in your `.env` file
