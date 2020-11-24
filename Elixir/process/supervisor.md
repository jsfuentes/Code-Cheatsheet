# Supervisors

## Dynamic Supervisors

Start genservers/process dynamically

*Supervisor won't restart if init fails, so use send self() for init*

```elixir 
#After start_link ing MySupervisor 
spec = %{id: PriceChecker, start: {PriceChecker, :start_link, [2]}}
DynamicSupervisor.start_child(MySupervisor, spec)
```

#### Spec Args

- `:id` - any term to identify the child specification internally (Required) 
- `:start` - a tuple with the module-function-args to be invoked to start the child process (Required)
- `:restart` 
  - `:permanent` - always restarted(Default)
  - `:temporary` - never restarted
  - `:transient` - restarted only if terminates abnormally (anything besides  `:normal`, `:shutdown`, or `{:shutdown, term}`)
- `:shutdown` - how to shutdown, defaults to `5_000` if the type is `:worker` or `:infinity` if the type is `:supervisor`.
- `:type` -  `:worker` (default) or a `:supervisor`

### Example

worker.ex

```elixir
defmodule ReactPhoenix.Dynamic.Recording do
  use GenServer

  def start_link(event_id) do
    name = {:via, Registry, {EventGenServer, "#{event_id}_recording"}}

    # wrap in :ok as start_link expects it 
    case GenServer.start_link(__MODULE__, event_id, name: name) do
      {:ok, pid} -> {:ok, pid}
      {:error, {:already_started, pid}} -> {:ok, pid}
      x -> x
    end
  end

  def init(state) do
    send(self(), :work)
    {:ok, state}
  end

  def handle_info(:work, state) do
    # do important stuff
    IO.puts("#{state} Important stuff in progress...")

    if state <= 20 do
      Process.send_after(self(), :work, 1000)
      {:noreply, state + 1}
    else
    	#will restart if restart strategy :permanent
      {:stop, :normal, state}
    end
  end
end

```

supervisor.ex

```elixir
defmodule ReactPhoenix.Dynamic.Supervisor do
  use DynamicSupervisor
  alias ReactPhoenix.Dynamic.Recording

  def start_link(_arg) do
    DynamicSupervisor.start_link(__MODULE__, :ok, name: __MODULE__)
  end

  def init(:ok) do
    DynamicSupervisor.init(strategy: :one_for_one)
  end

  def start_recording(event_id) do
    spec = %{id: Recording, start: {Recording, :start_link, [event_id]}}
    DynamicSupervisor.start_child(__MODULE__, spec)
  end
end
```

application.ex

```elixir
    children = [
      ReactPhoenix.PriceSupervisor,
```

Usage, test in console: 

```elixir
ReactPhoenix.PriceSupervisor.start_work
```

