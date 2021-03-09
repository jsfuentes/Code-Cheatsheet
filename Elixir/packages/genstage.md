# [Genstage](https://github.com/elixir-lang/gen_stage)

[Motivation](https://elixir-lang.org/blog/2016/07/14/announcing-genstage/) - Sending events between Elixir processes with back-pressure in a producer -> producer_consumer(transform) -> consumer

- **Producer** - recieve demand(from consumer) and generate events
- **Producer_Consumer** - Doesn't handle demand, but transform events data
- **Consumer** - Recieve final events

Demand is auto generated and you just need to `start_link` => `sync_subscribe`  multiple of the same type to parallelize

#### Producer

```elixir
alias Experimental.GenStage

defmodule A do
  use GenStage

  def init(counter) do
    {:producer, counter}
  end

  def handle_demand(demand, counter) when demand > 0 do
    # If the counter is 3 and we ask for 2 items, we will
    # emit the items 3 and 4, and set the state to 5.
    events = Enum.to_list(counter..counter+demand-1)

    # The events to emit is the second element of the tuple,
    # the third being the state.
    {:noreply, events, counter + demand}
  end
end
```

#### Producer_Consumer

```elixir
alias Experimental.GenStage

defmodule B do
  use GenStage

  def init(number) do
    {:producer_consumer, number}
  end

  def handle_events(events, _from, number) do
    events = Enum.map(events, & &1 * number)
    {:noreply, events, number}
  end
end
```

#### Consumer

```elixir
alias Experimental.GenStage

defmodule C do
  use GenStage

  def init(sleeping_time) do
    {:consumer, sleeping_time}
  end

  def handle_events(events, _from, sleeping_time) do
    # Print events to terminal.
    IO.inspect(events)

    # Sleep the configured time.
    Process.sleep(sleeping_time)

    # We are a consumer, so we never emit events.
    {:noreply, [], sleeping_time}
  end
end
```

### Connect

```elixir
{:ok, a} = GenStage.start_link(A, 0)    # starting from zero
{:ok, b} = GenStage.start_link(B, 2)    # multiply by 2
{:ok, c} = GenStage.start_link(C, 1000) # sleep for a second

GenStage.sync_subscribe(c, to: b)
GenStage.sync_subscribe(b, to: a)

# Sleep so we see events printed.
Process.sleep(:infinity)
```

### Parallelize

```elixir
{:ok, a} = GenStage.start_link(A, 0)     # starting from zero
{:ok, b} = GenStage.start_link(B, 2)     # multiply by 2

{:ok, c1} = GenStage.start_link(C, 1000) # sleep for a second
{:ok, c2} = GenStage.start_link(C, 1000) # sleep for a second
{:ok, c3} = GenStage.start_link(C, 1000) # sleep for a second
{:ok, c4} = GenStage.start_link(C, 1000) # sleep for a second

GenStage.sync_subscribe(c1, to: b)
GenStage.sync_subscribe(c2, to: b)
GenStage.sync_subscribe(c3, to: b)
GenStage.sync_subscribe(c4, to: b)
GenStage.sync_subscribe(b, to: a)

# Sleep so we see events printed.
Process.sleep(:infinity)
```

