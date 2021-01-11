# Oba[n](https://hexdocs.pm/oban/Oban.html)

Robust job processing in Elixir, backed by modern PostgreSQLFeatures

- Scheduled Jobs - at any time in future down to second
- CRON Jobs - Perodic jobs

- Queue Control - start, stop, scale independently
- Unique Jobs, Priority

See the `Oban.Worker` docs for more details on failure conditions and `Oban.Telemetry` for details on job reporting.

## Usage

### Defining Workers

Must define `perform/1` function with %Oban.Job{} struct

- args will always have string keys cuz serialization
- Successful jobs return `:ok` or `{:ok, value}` to treat as success, return other for failure, discard, deferred

```elixir
defmodule MyApp.Business do
  use Oban.Worker,
    queue: :events,
    priority: 3,
    max_attempts: 3,
    tags: ["business"],
    unique: [period: 30] #in seconds

  @impl Oban.Worker
  def perform(%Oban.Job{args: %{"id" => id} = args}) do
    #work hard grrrrr
    :ok
  end
end
```

### Enqueueing Jobs

Jobs are enqueued by inserting Ecto struct into db. All workers define a `new/2` function that serves as changest.

```elixir
%{id: 1, in_the: "business", of_doing: "business"}
|> MyApp.Business.new()
|> Oban.insert()
```

At specific future time

```elixir 
%{id: 1}
|> MyApp.Business.new(scheduled_at: ~U[2020-12-25 19:00:56.0Z])
|> Oban.insert()
```

#### Periodic Jobs

Has one minute resolution(will trigger within a minute)

```elixir
config :my_app, Oban, repo: MyApp.Repo, crontab: [
  {"* * * * *", MyApp.MinuteWorker},
  {"0 * * * *", MyApp.HourlyWorker, args: %{custom: "arg"}},
  {"0 0 * * *", MyApp.DailyWorker, max_attempts: 1},
  {"0 12 * * MON", MyApp.MondayWorker, queue: :scheduled, tags: ["mondays"]},
  {"@daily", MyApp.AnotherDailyWorker}
]
```

Jobs are considered unique for most of each minute, which prevents duplicate jobs with multiple nodes and across node restarts.

#### Unique Jobs

Uniqueness is based on a combination of `args`, `queue`, `worker`, `state` and insertion time.

Can be configured for worker

```elixir
use Oban.Worker, unique: [period: 60] #in seconds
```

Or for specific job

```elixir
%{email: "brewster@example.com"}
|> MyApp.Mailer.new(unique: [period: 300, fields: [:queue, :worker])
|> Oban.insert()
```

## Setup

1) Install oban dep

```elixir
    {:oban, "~> 2.3"}
```

2) Migration

```bash
mix ecto.gen.migration add_oban_jobs_table
```

Place the follow in the newly created migration

```elixir
	use Ecto.Migration

  def up do
    Oban.Migrations.up()
  end

  # We specify `version: 1` in `down`, ensuring that we'll roll all the way back down if
  # necessary, regardless of which version we've migrated `up` to.
  def down do
    Oban.Migrations.down(version: 1)
  end
```

```
mix ecto.migrate
```

3) Config

Config.exs

```elixir
config :my_app, Oban,
  repo: MyApp.Repo,
  plugins: [Oban.Plugins.Pruner],
  queues: [default: 10, events: 50, media: 20]
```

application.ex

```elixir
  def start(_type, _args) do
    children = [
      Repo,
      Endpoint,
      {Oban, oban_config()}
    ]

    Supervisor.start_link(children, strategy: :one_for_one, name: MyApp.Supervisor)
  end

  # Conditionally disable crontab, queues, or plugins here.
  defp oban_config do
    Application.get_env(:my_app, Oban)
  end
```

