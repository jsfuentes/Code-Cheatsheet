# Sentry

## Setup

Edit your mix.exs file to add it as a dependency and add the `:sentry` package to your applications:

```elixir
    {:sentry, "~> 8.0"},
    {:jason, "~> 1.1"},
```

#### Config

config/prod.exs

```elixir
config :sentry,
  dsn: "https://e9bdcefghij.ingest.sentry.io/5265101",
  environment_name: Mix.env(), #:prod 
  enable_source_code_context: true,
  root_source_code_path: File.cwd!,
  tags: %{
    env: "production"
  },
  included_environments: [:prod] #environment_name to send messages in
```

lib/react_phoenix_web/endpoint.ex

```elixir
defmodule ReactPhoenixWeb.Router do
  use ReactPhoenixWeb, :router
  use Plug.ErrorHandler
  use Sentry.Plug
  
  #........

  plug Sentry.PlugContext
  plug Plug.MethodOverride
  plug Plug.Head
  plug Plug.Session, @session_options
  plug ReactPhoenixWeb.Router
end
```

#### Logger.error

```elixir
config :logger, backends: [:console, Sentry.LoggerBackend]
#print all messages in prod
config :logger, :console, level: :debug 

#sentry capture all error messages
config :logger,
       Sentry.LoggerBackend,
       # Send messages like `Logger.error("error")` to Sentry
       capture_log_messages: true,
       # Also send warn messages like `Logger.warn("warning")` to Sentry
       # level: :warn,
       # Do not exclude exceptions from Plug/Cowboy
       excluded_domains: [],
       # Include metadata added with `Logger.metadata([foo_bar: "value"])`
       metadata: [:request_id]
```

## Usage

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

### Context

Complex because elixir processes isolated

```elixir
# Global Tags
config :sentry,
  tags: %{my_app_version: "14.30.10"}

# Process-based Context
Sentry.Context.set_extra_context(%{day_of_week: "Friday"})
Sentry.Context.set_user_context(%{id: 24, username: "user_username", has_subscription: true})
Sentry.Context.set_tags_context(%{locale: "en-us"})
Sentry.Context.add_breadcrumb(%{category: "web.request"})

# Event-based Context
Sentry.capture_exception(exception, [tags: %{locale: "en-us", }, user: %{id: 34},
  extra: %{day_of_week: "Friday"}, breadcrumbs: [%{timestamp: 1461185753845, category: "web.request"}]]
```

