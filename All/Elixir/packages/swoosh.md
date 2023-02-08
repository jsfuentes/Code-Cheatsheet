# Swoosh

Might come with phoenix now unclear

Config.exs

```elixir
# Configures the mailer
config :react_phoenix, ReactPhoenix.Mailer,
  adapter: Swoosh.Adapters.Postmark,
  api_key: System.get_env("POSTMARK_API_KEY")

# Swoosh API client is needed for adapters other than SMTP.
config :swoosh, :api_client, Swoosh.ApiClient.Hackney
```

ReactPhoenix.Mailer

```elixir
defmodule ReactPhoenix.Mailer do
  use Swoosh.Mailer, otp_app: :react_phoenix
end
```

