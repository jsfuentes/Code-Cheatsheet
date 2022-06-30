# [Logger](https://hexdocs.pm/logger/Logger.html)

It includes many features:

- Provides debug, info, warn, and error levels.
- Supports multiple backends which are automatically supervised when plugged into [`Logger`](https://hexdocs.pm/logger/master/Logger.html#content).
- Formats, truncates, and alternates between async/sync when under stress to avoid clogging [`Logger`](https://hexdocs.pm/logger/master/Logger.html#content) backends.
- Integrates with Erlang's [`:logger`](http://erlang.org/doc/man/logger.html) to convert terms to Elixir syntax.
- Automatically includes metadata like :application, :mfa(module function and arity), :file, :line, :pid, :crash_reason etc
- **Advanced**: Format and include more information in prod

## Usage

Note the arguments given to [`info/2`](https://hexdocs.pm/logger/Logger.html#info/2) will only be evaluated if a message is logged(its a high enough log level)

```elixir
  require Logger
  
  # Every log call in this process will have this metadata
  Logger.metadata(request_id: request_id)
  # 2nd arg is metadata
  Logger.info("Successfully processed payment", confirmation_code: c)
  #......
	Logger.info("Deleting user from the system: #{inspect(user)}")
```

Levels, setting logger to any level will show all above too

- `:emergency` - when system is unusable, panics
- `:alert` - for alerts, actions that must be taken immediately, ex. corrupted database
- `:critical` - for critical conditions
- `:error` - for errors
- `:warning` - for warnings
- `:notice` - for normal, but signifant, messages
- `:info` - for information of any kind
- `:debug` - for debug-related messages

## Config

```elixir
# Our Logger general configuration
config :logger,
  backends: [:console],
  compile_time_purge_level: :debug

# Our Console Backend-specific configuration
config :logger, :console,
  format: "\n##### $time $metadata[$level] $levelpad$message\n",
  metadata: :all
```

