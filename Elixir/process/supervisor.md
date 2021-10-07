# Supervisors

*“In a supervision hierarchy, keep important application state or functionality near the root while delegating risky operations towards the leaves.”* - Error Kernel

If the child of a supervisor fails to restart `max_restarts` times in `max_seconds`, then the SUPERVISOR crashes. This means if a child of the application supervisor crashes, the ENTIRE APPLICATION will crash.

So yes fail if there are issues, but [the known state should actually work](https://ferd.ca/it-s-about-the-guarantees.html).

## Dynamic Supervisors

Works well with Registry to limit to one per or something

### Init

```elixir
defmodule ReactPhoenix.Dynamic.Supervisor do
  use DynamicSupervisor

  def init(:ok) do
    DynamicSupervisor.init(strategy: :one_for_one)
  end
  
  #.....
end
```

- `:strategy` - Currently only  `:one_for_one` , where a child process terminates doesnt affect other children
- `:max_restarts` - max restarts allowed in max_seconds. Default `3`  
- `:max_seconds` - the time frame in which `:max_restarts` applies. Defaults  `5`.
- `:max_children` - the maximum amount of children to be running under this supervisor at the same time. When `:max_children` is exceeded, [`start_child/2`](https://hexdocs.pm/elixir/1.12/DynamicSupervisor.html#start_child/2) returns `{:error, :max_children}`. Defaults to `:infinity`.
- `:extra_arguments` - arguments prepended to the child spec given to [`start_child/2`](https://hexdocs.pm/elixir/1.12/DynamicSupervisor.html#start_child/2)

application.ex

```elixir
      children=[
      ....,
      {Registry, keys: :unique, name: Registry.EventFolderGenServer},
      ReactPhoenix.Dynamic.EventFolderSupervisor,
```



### Start Child

Start genservers/process dynamically

*Supervisor won't restart if init fails, so use send self() for init*

#### Way 1 Child Spec

```elixir
DynamicSupervisor.start_child(MySupervisor, Stack)
DynamicSupervisor.start_child(MySupervisor, {Stack, [:hello]})
```

`use GenServer` , agent, or supervisor all define default child_spec as below

```elixir
def child_spec(arg) do
	%{id: Stack, start: {Stack, :start_link, [arg]}
end
```

Can modify child_spec options directly in the use

```elixir
use GenServer, restart: transient
```

#### Way 2 Direct Spec 

```elixir 
spec = %{
	id: PriceChecker, 
	start: {PriceChecker, :start_link, [2]}
}

DynamicSupervisor.start_child(MySupervisor, spec)
```

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

