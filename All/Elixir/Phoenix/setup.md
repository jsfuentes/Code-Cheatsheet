# Setup

#### Installation

```bash
mix archive.install hex phx_new
```

### Setup

1. Create Boilerplate

```bash
mix phx.new react_phoenix
```

Flags: 

- `--no-ecto` to not have database stuff

2. Create secrets in `.env` and db secrets

   ```bash
   mix phx.gen.secret
   ```

   .env - need to move db config to `.config.ex`

   ```bash
   export DB_USERNAME="test_user"
   export DB_PASSWORD="LONGTESTPASSWORD"
   export DB_DATABASE="pi_test"
   export DB_HOSTNAME="SOMELONGTHING.oregon-postgres.render.com"
   export SECRET_KEY_BASE="SOMEExTREMELYLONGSECRETKE"
   ```

3. 

Follow steps it prompts you with, then start with:

```bash
mix phx.server 
iex -S mix phx.server #interactive run, `recompile()`, can run all the models like Ss.Accounts.list_users
```

Phoenix uses webpack or esbuild for asset management and needs npm*

Main work will be in lib

### DB

Local: idk. By Postgres default, the username is the default machine name like jfuentes(`whoami` in bash)  and no password ""

AWS: Before running `mix ecto.create` go into `config/dev.ex` and change the db connection settings to the AWS one. Creates a database of that name if it doesn't exist
