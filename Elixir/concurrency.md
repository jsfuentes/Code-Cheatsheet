### Concurrency

- As easy as `spawn` to  runs code specified at undefined time each with a process_id
- Send messages between processes

```elixir
spawn(fn() -> loop(50, 1) end) # loop defined up there
spawn(fn() -> loop(100, 50) end)
send(self(), {:french, "Bob"})

receive do 
	{:german, name} -> IO.puts "Guten tag #{name}"
	{:french, name} -> IO.puts "Bonjour #{name}"
	after
	500 -> IO.puts "Time up"
end
```

Message Passing

```elixir
current_process = self()

# Spawn an Elixir process (not an operating system one!)
spawn_link(fn ->
  send(current_process, {:msg, "hello world"})
end)

# Block until the message is received
receive do
  {:msg, contents} -> IO.puts(contents)
end
```

