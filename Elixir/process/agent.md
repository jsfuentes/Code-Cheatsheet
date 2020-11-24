# Agent

Simple wrapper of genserver for state

-  creates child_spec/1 function that start agent directly under a supervisor.
-  **single threaded state management**, updates require new object(ETS much more scalable, but agent good for smaller use cases)
-  genserver with specific functions for get, update, cast that operate on state and combining server and client code into one function

```elixir
defmodule Counter do
  use Agent 

  def start_link(initial_value) do
    Agent.start_link(fn -> initial_value end, name: __MODULE__)
  end

  def value do
  	#gets agent state, applies ft, then returns
    Agent.get(__MODULE__, & &1)
  end

  def increment do
  	#applies ft to the state and updates it
    Agent.update(__MODULE__, &(&1 + 1)) 
  end
end
```

Usage

```elixir
Counter.start_link(0) #=> {:ok, #PID<0.123.0>}
Counter.value() #=> 0
Counter.increment() #=> :ok
Counter.increment() #=> :ok
Counter.value() #=> 2
```

#### Considerations

- Atomic updates because server fns run one by one
+ Should therefore put long running processes in client(not inside agent ft calls), because it will block the agent from recieving other calls from other processes

#### Raw

Keep a process running that loops infinitely maintaining state and sending/recieving messages

```elixir
defmodule KV do
  def start_link do
    Task.start_link(fn -> loop(%{}) end)
  end

	#defp makes it private
  defp loop(map) do
    receive do
      {:get, key, caller} ->
        send caller, Map.get(map, key)
        loop(map)
      {:put, key, value} ->
        loop(Map.put(map, key, value))
    end
  end
end
```

Can then register a pid giving it a name avaliable to all

```elixir
Process.register(pid, :kv)
send :kv, {:get, :hello, self()}
```

