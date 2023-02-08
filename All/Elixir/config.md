# Config

Each application has its own environment. 

`config/config.exs`  is base of every project 

config/dev.exs

```elixir
import_config "dev.secret.exs"
```

config/dev.secrets.exs

```elixir
use Mix.Config

config :sonar,
  google: "fasfdajkl"
```

#### Usage

```elixir
Application.fetch_env!(:sonar, :google)
Application.get_env(:sonar, :google, :default) #allows default and no error if key doesn't exist
```

### Based on env

```elixir
  if Mix.env() == :dev do
    #... can even be in router
  end
```

## Runtime.ex vs Prod.ex

Simply:

- `releases.exs` - runtime configuration for `release` **only**
- `#{Mix.env()}.exs` - i.e. `dev.exs`, `prod.exs`, `test.exs` - those are compiletime environment-specific configuration files
- `config.exs` - compiletime generic configuration file
- `releases.exs` - runtime generic configuration file
