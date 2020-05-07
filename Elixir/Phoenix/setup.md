#Setup

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

```bash
mix phx.gen.html [Context] [Schema] [schema_plural]  [field1] [field2] [....]#building a page
mix phx.gen.json #building an api
mix phx.gen.channel #building a channel
mix phx.gen.context #just db stuff?
```

#### Examples

By default, its a string could make it `name:string` if you want though

```bash
mix phx.gen.html Accounts User users name username:unique
mix phx.gen.context Accounts Credential credentials email:unique password_hash user_id:references:users
mix phx.gen.html Chat Room rooms name:unique description:text user_id:references:users
```

### Running

