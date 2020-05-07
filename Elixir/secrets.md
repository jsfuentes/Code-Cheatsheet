# Secrets

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

Elsewhere

```elixir
Application.fetch_env!(:external_service, :google)
```

