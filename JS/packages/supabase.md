# [Supabase](https://supabase.com/docs)

Open source Firebase giving client side ORM that directly accesses DB, can listen for changes

- Can generate types with `supabase gen types typescript --project-id abcdefghijklmnopqrst > database.types.ts`
- Railway

## Setup

```js
import { createClient } from '@supabase/supabase-js'

const supabase = createClient(supabase_url, anon_key)
```

## Querying

```js
//basic query
const { data, error } = await supabase
  .from('cities')
  .select('name, country_id')
  .gte('population', 1000)
  .lt('population', 10000)
  
//if politician has an id linking to ballot_item or its through a composite key join table(nothing needs to be set to differentiate)
  const { data, error } = await supabase.from("ballot_item").select(`
    *,
    politician (*)
  `)
  .eq('politician.first_name', 'Donald');
  
//query JSON
const { data, error } = await supabase
  .from('users')
  .select(`
    id, name,
    address->city
  `)
```

Can add [filters](https://supabase.com/docs/reference/javascript/using-filters) to match a pattern, greater less then, in an array etc.

Can add [modifiers](https://supabase.com/docs/reference/javascript/using-modifiers) like `.order(), .upsert()`

### Insert

```js
//create and return
const { data, error } = await supabase
  .from('countries')
  .insert({ id: 1, name: 'Denmark' })
  .select()
```



### Postgres Functions

```js
const { data, error } = await supabase.rpc('hello_world')
```

### Extra

- If you want to do an upsert based on multiple column uniqueness, need to create multicolumn unique index in SQL Editor with `CREATE UNIQUE INDEX user_date ON voter_guide(user_id, election_date);`
