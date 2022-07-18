# Generators

Used as learning tools for both db as well as channel/migrations

#### Examples

```bash
mix phx.gen.json Boards Board boards owner_id:references:users title description

mix phx.gen.context Templates Template templates event_id:references:events description preview

mix phx.gen.context Templates TemplateXTag templates_x_tags template_id:references:templates template_tag_id:references:template_tags

mix phx.gen.context Templates TemplateTag template_tags name
```

- No :type means it is a :string, but use :text if >256 chars
- Often need to modify schema to have belong_to/has_many/has_one
- Need to change migration if id type is string or 

## General Usage

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

Finalize in db

```bash
mix ecto.migrate
```

Other

```bash
mix phx.gen.channel [module_name] #adds channel to name
mix phx.gen.migration [Migration Name]
```

### Advanced, Default to Binary_ID

BinaryID is uuid letting you generate ids on the client

Config.exs

```elixir
config :react_phoenix,
  ecto_repos: [ReactPhoenix.Repo],
  generators: [binary_id: true] #default to binary_id
```

