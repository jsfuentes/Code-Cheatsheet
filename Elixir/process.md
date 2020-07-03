# Processes / Concurrency

- As easy as `spawn` to  runs code specified at undefined time each with a process_id
- Only communication is messages between processes
- Supervisors often linked to processes and will restart on failure
- [Agent](https://hexdocs.pm/elixir/Agent.html) - Simple wrappers around genserver for state. 
- [GenServer](https://hexdocs.pm/elixir/GenServer.html) - “Generic servers” (processes) that encapsulate state, provide sync and async calls, support code reloading, and more. For ongoing background work 
- [Task](https://hexdocs.pm/elixir/Task.html) - Asynchronous units of computation that allow spawning a process and potentially retrieving its result at a later time.

#### Spawn

```elixir
spawn(fn() -> loop(50, 1) end) # loop defined up there
spawn(fn() -> loop(100, 50) end)
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


