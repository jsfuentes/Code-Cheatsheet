# Registry

[Announcement](https://elixirforum.com/t/proposing-registry/2121)

```elixir
  children = [
    # ...
    {Registry, keys: :unique, name: GreeterRegistry}
```

### Usage

#### Registering

```elixir
defmodule ReactPhoenix.Dynamic.Recording do
  use GenServer

  def start_link(event_id),
    do: GenServer.start_link(__MODULE__, event_id, name: process_name(event_id))
    # {:error, {:already_started, current_pid}}. if already defined

  defp process_name(person),
    do: {:via, Registry, {EventGenServer, "#{event_id}_recording"}}

```

#### Lookup

```elixir
Registry.lookup(GreeterRegistry, "agent")


```

