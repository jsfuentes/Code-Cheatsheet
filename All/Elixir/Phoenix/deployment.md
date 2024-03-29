# Deployment

Make sure your configuration works in the prod files including the url host and any .env variables are ready

```bash
# Initial setup
mix deps.get --only prod
MIX_ENV=prod mix compile

# Compile assets
npm run deploy --prefix ./assets
mix phx.digest #digest/cache manifest to quickly serve assets in prod
```

Running

```bash
PORT=4001 MIX_ENV=prod mix phx.server
#In detached mode:
PORT=4001 MIX_ENV=prod elixir --erl "-detached" -S mix phx.server
```

## [Releases](https://hexdocs.pm/phoenix/releases.html)

Can make a bundle with Elixir, Erlang VM, and code that you can drop on a prod machine/docker container and run.

### Gen

`mix phx.gen.release` apparently needed for something like running migrations in the release idk its in the guide

```elixir
# Initial setup
mix deps.get --only prod
MIX_ENV=prod mix compile

# Compile assets
npm install --prefix ./assets
npm run deploy --prefix ./assets
mix phx.digest

# Build the release and overwrite the existing release directory
MIX_ENV=prod mix release --overwrite
```

Then using this built release

```bash
# Running
_build/prod/rel/react_phoenix/bin/react_phoenix start

# All commands
_build/prod/rel/react_phoenix/bin/react_phoenix

# Accessing while running(after ssh?)
_build/prod/rel/react_phoenix/bin/react_phoenix remote
```

### [Heroku](https://hexdocs.pm/phoenix/heroku.html)

Need 2 buildpacks, config the version of elixir and erlang, configure config.exs

```bash
heroku create --buildpack hashnuke/elixir #will return url to use in prod
heroku buildpacks:add https://github.com/gjaldon/heroku-buildpack-phoenix-static.git
```

config/prod.exs

```elixir
config :react_phoenix, ReactPhoenixWeb.Endpoint,
  http: [port: {:system, "PORT"}],
  url: [scheme: "https", host: "mysterious-meadow-6277.herokuapp.com", port: 443],
  cache_static_manifest: "priv/static/cache_manifest.json"
```

elixir_buildpack.config

```bash
elixir_version=1.10.1

# available versions https://github.com/HashNuke/heroku-buildpack-elixir-otp-builds/blob/master/otp-versions
erlang_version=21.2.5
```

phoenix_static_buildpack.config

```bash
node_version=12.14.1
```

[Can let phoneix handle http to https](https://hexdocs.pm/phoenix/using_ssl.html#force-ssl)

Now you want to make sure elixir closes connections instead of heroku

endpoint.ex

```elixir
  socket "/socket", ReactPhoenixWeb.UserSocket,
    websocket: [timeout: 45_000],
    longpoll: false
```

Finally, generate a new secret and set it in Herkou

```bash
mix phx.gen.secret
```

```bash
heroku config:set SECRET_KEY_BASE="xvafzY4y01jYuzLm3ecJqo008dVnU3CN4f+MamNd1Zue4pXvfvUjbiXT8akaIF53"
```

Limitations: 

- Connections limits simultaneous connections
- Firewalls dynos so distributed channels/tasks need to backup on Redis instead of Elixir
- Inmemory states will be lost every 24 hours
- No observer

