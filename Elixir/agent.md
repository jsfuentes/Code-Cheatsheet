## Agent

Abstraction for raw implementation of an infinite process that maintains state

-  creates child_spec/1 function that start agent directly under a supervisor.
-  should think about putting long running processes in client(not inside agent calls), because it will block the agent from recieving other calls from other processes

```elixir
defmodule Counter do
  use Agent 

  def start_link(initial_value) do
    Agent.start_link(fn -> initial_value end, name: __MODULE__)
  end

  def value do
    Agent.get(__MODULE__, & &1)
  end

  def increment do
    Agent.update(__MODULE__, &(&1 + 1)) #any ft that takes state and returns new state
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

