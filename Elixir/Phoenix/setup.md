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
