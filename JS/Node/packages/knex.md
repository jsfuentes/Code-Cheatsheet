# Knex

SQL query builder 

`npm install knex`

## Initialization

Initializing the Library

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
knex('users').where('id', 1)
const results = await knex.select()
												.from('_plugin_logs');
knex('accounts')
  .where('activated', false)
  .del()
```

```javascript
knex({ a: 'table', b: 'table' })
  .select({
    aTitle: 'a.title',
    bTitle: 'b.title'
  })
  .whereRaw('?? = ??', ['a.column_1', 'b.column_2'])
```

## Where

```js
knex('users').where({
  first_name: 'Test',
  last_name:  'User'
}).select('id')
knex('users').where('id', 1)
```

## Order

```js
knex('users').orderBy('email')
knex('users').orderBy('name', 'desc')
```

