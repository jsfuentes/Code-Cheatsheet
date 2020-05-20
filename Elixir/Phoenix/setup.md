# Setup

```bash
iex -S mix phx.server
```

#### Installation

```bash
mix archive.install hex phx_new 1.5.1 #maybe dif v
```

#### Boilerplate

```bash
mix phx.new hello
```

Flags: 

- `--no-ecto` to not have database stuff

Follow steps it prompts you with, then start with:

```bash
mix phx.server 
iex -S mix phx.server #interactive run, `recompile()`, can run all the models like Ss.Accounts.list_users
```

Phoenix uses webpack for asset management and needs npm*

Main work will be in lib

### DB

Local: idk. By Postgres default, the username is the default machine name like jfuentes(`whoami` in bash)  and no password ""

AWS: Before running `mix ecto.create` go into `config/dev.ex` and change the db connection settings to the AWS one. Creates a database of that name if it doesn't exist

### Generators

Used as learning tools

Generating a schema in increasing complexity

```bash
mix phx.gen.schema [Schema] [schema_plural]  [field1] [field2] [....] #just schema and migration
mix phx.gen.context [Context] [Schema...] #all + context
mix phx.gen.json [....] #all of above + resource
mix phx.gen.html [Context]  #all of above + html
```

Other

```bash
mix phx.gen.channel [Module_Name_for_channel]
mix phx.gen.migration [Migration Name]
```

#### Examples

By default, its a string could make it `name:string` if you want though

```bash
mix phx.gen.html Accounts User users name username:unique
mix phx.gen.context Accounts Credential credentials email:unique password_hash user_id:references:users
mix phx.gen.html Chat Room rooms name:unique description:text user_id:references:users
```

### Deployment

https://hexdocs.pm/phoenix/releases.html