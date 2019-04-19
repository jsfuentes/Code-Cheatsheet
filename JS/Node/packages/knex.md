# Knex

SQL query builder 

`npm install knex`

## Initialization

Initializing the Library
The knex module is itself a function which takes a configuration object for Knex, accepting a few parameters. The client parameter is required and determines which client adapter will be used with the library.

```js
var knex = require('knex')({
  client: 'mysql',
  connection: {
    host : '127.0.0.1',
    user : 'your_database_user',
    password : 'your_database_password',
    database : 'myapp_test'
  }
});
```

## Usage

### Insert

```javascript
await knex('_plugin_logs').insert(req.body);
```

### Query

```javascript
knex({ a: 'table', b: 'table' })
  .select({
    aTitle: 'a.title',
    bTitle: 'b.title'
  })
  .whereRaw('?? = ??', ['a.column_1', 'b.column_2'])
```

