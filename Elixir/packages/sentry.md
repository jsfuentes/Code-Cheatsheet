# Sentry

## Setup

Edit your mix.exs file to add it as a dependency and add the `:sentry` package to your applications:

```elixir
    {:sentry, "~> 7.0"},
    {:jason, "~> 1.1"},
```

#### Config

config/prod.exs

```elixir
config :sentry,
  dsn: "https://e9bdc39cd1ca436b809b5c9a8d5518ac@o353677.ingest.sentry.io/5265101",
  environment_name: :prod,
  enable_source_code_context: true,
  root_source_code_path: File.cwd!,
  tags: %{
    env: "production"
  },
  included_environments: [:prod] #environment_name to send messages in
```

**Alternative** is general config file  `Mix.env`

```elixir
config :sentry, dsn: "https://e9bdc39cd1ca436b809b5c9a8d5518ac@o353677.ingest.sentry.io/5265101",
   included_environments: [:prod],
   environment_name: Mix.env
```

Relies on Mix.env being `:prod`

**Phoenix**  or Plug envs should use the following to Plug.Router or Phoenix.Router: 

lib/react_phoenix_web/router.ex

```elixir
defmodule ReactPhoenixWeb.Router do
  use ReactPhoenixWeb, :router
  use Plug.ErrorHandler
  use Sentry.Plug
```

lib/react_phoenix_web/endpoint.ex

```elixir
defmodule ReactPhoenixWeb.Endpoint do
  use Phoenix.Endpoint, otp_app: :react_phoenix
  use Sentry.Phoenix.Endpoint
  
```

## Capturing Errors

If you use the LoggerBackend and set up the Plug/Phoenix integrations, all errors will bubble up to Sentry.

Otherwise, we provide a simple way to capture exceptions manually:

```elixir
try do
  ThisWillError.really()
rescue
  my_exception ->
    Sentry.capture_exception(my_exception, [stacktrace: __STACKTRACE__, extra: %{extra: information}])
end
```

### Messages

```elixir
Sentry.capture_message("custom_event_name", extra: %{extra: information})

```

