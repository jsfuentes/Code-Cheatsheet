# Config

Hierarchical configurations for your app: 

- Set with  ` export NODE_ENV=production` 
- Uses the default configuration values unless the production one explicitly has a value for that key

```bash
npm install config
mkdir config
emacs config/default.json
```

default.json

```
{
  // Customer module configs
  "Customer": {
    "dbConfig": {
      "host": "localhost",
      "port": 5984,
      "dbName": "customers"
    },
    "credit": {
      "initialLimit": 100,
      // Set low for development
      "initialDays": 1
    }
  }
}
```

**Edit config overrides for production deployment:**

`emacs config/production.json`

```
{
  "Customer": {
    "dbConfig": {
      "host": "prod-db-server"
    },
    "credit": {
      "initialDays": 30
    }
  }
}
```

**Use configs in your code:**

```
const config = require('config');
//...
const dbConfig = config.get('Customer.dbConfig');
db.connect(dbConfig, ...);
 
if (config.has('optionalFeature.detail')) {
  const detail = config.get('optionalFeature.detail');
  //...
}
```

`config.get()` will throw an exception for undefined keys to help catch typos and missing values. Use `config.has()` to test if a configuration value is defined.

**Start your app server:**

```bash
export NODE_ENV=production
node my-app.js
```

Running in this configuration, the `port` and `dbName` elements of `dbConfig` will come from the `default.json` file, and the `host` element will come from the `production.json`override file.