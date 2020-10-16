# Generators

Think about how to auto make the foreign keys cascade

mix phx.gen.schema ChatChannel chat_channels user_id:references:users event_id:references:events subevent_id:references:subevents group_id type

Used as learning tools

Generating a schema in increasing complexity

```bash
mix phx.gen.schema [SchemaSingluar] [schema_plural]  [field1] [field2] [....] #just schema and migration
mix phx.gen.context [Context] [Schema...] #all + context
mix phx.gen.json [....] #all of above + controller
mix phx.gen.html [Context]  #all of above + html
```

**Types**: `:integer` | `:float` |`:decimal` |`:boolean` |`:map` (Will convert to string keys)|`:string`(255 char limit use text instead) |`:array`  |`:references` |`:text`(In ecto schema still string type) |`:date` | `:time` |`:time_usec` |`:naive_datetime` |`:naive_datetime_usec` |`:utc_datetime` |`:utc_datetime_usec` |`:uuid` |`:binary` |`:datetime` 

#### DataTime Types

Only difference is the conversion to elixir, same DB type

| type                | precision | Elixir type                                                  | timezone |
| ------------------- | --------- | ------------------------------------------------------------ | -------- |
| naive_datetime      | sec       | [`NaiveDateTime`](https://hexdocs.pm/elixir/NaiveDateTime.html) | None     |
| naive_datetime_usec | microsec  | [`NaiveDateTime`](https://hexdocs.pm/elixir/NaiveDateTime.html) | None     |
| utc_datetime        | sec       | [`DateTime`](https://hexdocs.pm/elixir/DateTime.html)        | UTC      |
| utc_datetime_usec   | microsec  | [`DateTime`](https://hexdocs.pm/elixir/DateTime.html)        | UTC      |

#### Examples

No :type means it is a :string

```bash
mix phx.gen.context Accounts User users name email:unique bio number_of_pets:integer post_id:references:posts

mix phx.gen.context Accounts Credential credentials email:unique password_hash user_id:references:users

mix phx.gen.html Chat Room rooms name:unique description:text user_id:references:users
```

Finalize in db

```bash
mix ecto.migrate
```

Other

```bash
mix phx.gen.channel [module_name] #adds channel to name
mix phx.gen.migration [Migration Name]
```


