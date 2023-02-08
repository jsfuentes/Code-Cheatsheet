# Processes / Concurrency

- As easy as `spawn` to  runs code specified at undefined time each with a process_id
- Only communication is messages between processes
- Supervisors often linked to processes and will restart on failure
- [Agent](https://hexdocs.pm/elixir/Agent.html) - Simple wrappers around genserver for state. 
- [GenServer](https://hexdocs.pm/elixir/GenServer.html) - “Generic servers” (processes) that encapsulate state, provide sync and async calls, support code reloading, and more. For ongoing background work 
- [Task](https://hexdocs.pm/elixir/Task.html) - Asynchronous units of computation that allow spawning a process and potentially retrieving its result at a later time.
- DynamicSupervisors - Allow you to dynamically create and restart/supervise agents/genservers like if you need to spin one up per user or event
- [Registry](https://hexdocs.pm/elixir/Registry.html) - Allow strings to map to processes(instead of just atoms) 

#### Spawn

```elixir
spawn(fn() -> loop(50, 1) end) # loop defined up there
spawn(fn() -> loop(100, 50) end)
spawn(MODULE_NAME, FUNCTION_NAME, [ARGS])#alt

spawn_link(fn() -> :ok end) #spawn_link means if one process exits the other one will too(stops dangling p's)
```

#### Message Passing

- messages are only one way, so if want response need to recieve

- Messages will be put in process mailbox for future use

```elixir
send(self(), {:french, "Bob"})

# Block until a message is received
receive do 
	{:german, name} -> IO.puts "Guten tag #{name}"
	{:french, name} -> IO.puts "Bonjour #{name}"
	after
	500 -> IO.puts "Time up"
end
```

### Process Investigate

Look at livedashboard or erlang observer or

```elixir
pid = Process.list |> Enum.random
Process.info(p)
Process.alive?(p)
```

```
[
  current_function: {:prim_inet, :accept0, 3},
  initial_ call: {:ranch_acceptor, :loop, 4},
  status: :waiting,
  message_queue_len: 0,
  links: [#PID<0.435.0>],
  dictionary: [],
  trap_exit: false,
  error_handler: :error_handler,
  priority: :normal,
  group_leader: #PID<0.386.0>,
  total_heap_size: 233,
  heap_size: 233,
  stack_size: 14,
  reductions: 36,
  garbage_collection: [
    max_heap_size: %{error_logger: true, kill: true, size: 0},
    min_bin_vheap_size: 46422,
    min_heap_size: 233,
    fullsweep_after: 65535,
    minor_gcs: 0
  ],
  suspending: []
]
```

### Process Monitor

```elixir
iex> {:ok, pid} = KV.Bucket.start_link([])
{:ok, #PID<0.66.0>}
iex> Process.monitor(pid)
#Reference<0.0.0.551>
iex> Agent.stop(pid)
:ok
iex> flush()
{:DOWN, #Reference<0.0.0.551>, :process, #PID<0.66.0>, :normal}
```

