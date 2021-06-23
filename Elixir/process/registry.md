# Registry

[Announcement](https://elixirforum.com/t/proposing-registry/2121)

```elixir
  children = [
    # ...
    {Registry, keys: :unique, name: Registry.EventGenServer, partitions: System.schedulers_online()}
```

Partitions apparently makes it more concurrent if needed(Note that the registry uses one ETS table plus two ETS tables per partition.)

### Usage

#### Registering

start_link with the name to register in Registry

```elixir
  def start_link({cname, event_id, subevent_id, group_id}) do
    name = {:via, Registry, {EventGenServer, cname}}

    # seems to be :ok to return pid to supervisor
    case GenServer.start_link(__MODULE__, {cname, event_id, subevent_id, group_id}, name: name) do
      {:ok, pid} -> {:ok, pid}
      {:error, {:already_started, pid}} -> {:ok, pid}
    end
  end
```

#### Other

```elixir
name = {:via, Registry, {Registry.ViaTest, "agent"}}
{:ok, _} = Agent.start_link(fn -> 0 end, name: name)
```

#### Lookup

```elixir
Registry.lookup(GreeterRegistry, "agent")
```

#### Dispatch

```elixir
{:ok, _} = Registry.start_link(keys: :duplicate, name: Registry.DispatcherTest)

{:ok, _} = Registry.register(Registry.DispatcherTest, "hello", {IO, :inspect})

Registry.dispatch(Registry.DispatcherTest, "hello", fn entries ->
  for {pid, {module, function}} <- entries, do: apply(module, function, [pid])
end)
# Prints #PID<...> where the PID is for the process that called register/3 above
```

### Pubsub

Registries can also be used to implement a local, non-distributed, scalable PubSub by relying on the [`dispatch/3`](https://hexdocs.pm/elixir/1.11.4/Registry.html#dispatch/3)

```elixir
{:ok, _} = Registry.register(Registry.PubSubTest, "hello", [])

Registry.dispatch(Registry.PubSubTest, "hello", fn entries ->
  for {pid, _} <- entries, do: send(pid, {:broadcast, "world"})
end)
```

Can also use `Genserver.call/2` with the name to send direct message

```elixir
def speaker_layout(cname, maxResolutionUid) do
  name = {:via, Registry, {EventGenServer, cname}}
  GenServer.call(name, {:speaker_layout, maxResolutionUid})
end
```

