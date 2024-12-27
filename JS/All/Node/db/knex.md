# Knex

SQL query builder, install plugins like pg lib separately

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

### Select

```javascript
await knex.select('title', 'author').from('books') 
#Only first record
await knex.first('title', 'author').from('books') 
```

select returns a list of json

first returns a single json

if no entry, returns undefined or empty list

### Insert

```javascript
await knex('_plugin_logs').insert(req.body);
```

Add `.returning('*')` to return data 

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

### Where

```js
knex('users').where({
  first_name: 'Test',
  last_name:  'User'
}).select('id')

knex('users')
  .where('votes', '>', 100)
  .andWhere('status', 'active')
```

### Order

```js
knex('users').orderBy('email')
knex('users').orderBy('name', 'desc')
```

### Update

```js
knex('books')
  .where('published_date', '<', 2000)
  .update({
    status: 'archived',
    thisKeyIsSkipped: undefined
  })
```

returns true on success confirmed, idk else

Add `.returning('*')` to return data 

```js
knex('moderator').update({...moderator}).where({id}).returning('*')
```

### Count

```js
const greetingCount = await knex('phrase')
	.count()
	.where('intent', GREETING);

//[ { count: '1' } ]
```

### Join

```js
knex('users')
  .join('contacts', 'users.id', '=', 'contacts.user_id')
  .select('users.id', 'contacts.phone')
```

