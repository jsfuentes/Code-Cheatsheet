# Cron

Running recurring tasks at a specific time or interval

https://stackoverflow.com/questions/32085258/how-can-i-schedule-code-to-run-every-few-hours-in-elixir-or-phoenix-framework/32097971#32097971

```elixir
defmodule ReactPhoenix.PriceChecker do
  use GenServer

  def start_link(_) do
    GenServer.start_link(__MODULE__, 1)
  end

  def init(state) do
    :timer.send_interval(1000, :work)
    #could use Process.send_after for work that could take longer than interval
    {:ok, state}
  end

  def handle_info(:work, state) do
    # do important stuff
    IO.puts "#{state} Important stuff in progress..."
    {:noreply, state + 1}
  end
end
```

Application.ex

```elixir
    children = [
      ReactPhoenix.PriceChecker,
```

## Check out

Quantum for spinning up tasks during runtime(https://github.com/sickill/quantum-elixir/blob/master/pages/runtime.md) and doing a nice config of all of them

https://hexdocs.pm/oban/Oban.html for storing in db for better distributed systems