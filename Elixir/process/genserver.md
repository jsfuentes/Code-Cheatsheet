# GenServer (Generic Server)

- Great for scheduled/cron jobs, best to have it create a new process for doing work and just handling scheduling
- Start seperate process that holds some state, changes its state based on **calls**(sync expecting response) or **casts**(async, no resp) 
- Can recieve other/more messages than agent with handle_info

```elixir
defmodule SimpleGen do
  use GenServer
  @interval 1_000
  def start_link() do
    # runs in the caller context 🐌Alice
    GenServer.start_link(__MODULE__, [])
  end
  def init(_) do
    # runs in the server context 🐨Bob
    Process.send_after(self(), :increment, @interval)
    {:ok, 1}
  end
  def handle_info(:work, state) do
  	#some scheduled work
    Process.send_after(self(), :increment, @interval)
    {:noreply, state}
  end
  def handle_call(:get_data, _from, state) do
    # runs in the server context 🐨Bob
    {:reply, state, state}
  end
  def handle_cast(:increment, state) do
    # runs in the server context 🐨Bob
    {:noreply, state+1}
  end
end
```

### Usage

`start_link(module, init_arg, options \\ [])` calls init of the module with the init_args

```elixir
{:ok, pid} = GenServer.start_link() #starts new linked process(one dies both die)

counter = GenServer.call(pid, :get_data) #sync/blocking, default timeout 5 sec
IO.puts "Counter: #{counter}"
GenServer.cast(pid, :increment)
counter = GenServer.call(pid, :get_data)
IO.puts "Counter: #{counter}
```

- Don't use Process.sleep, instead will have to store data in state, use `:timer.after` to send message after time and process/complex work in handler

#### Raw Example without GenServer

```elixir
defmodule SimpleGenServerMock do
   def start_link() do
       # runs in the caller context 🐌Alice
       spawn_link(__MODULE__, :init, [])
   end
   def call(pid, arguments) do
       # runs in the caller context 🐌Alice
       send pid, {:call, self(), arguments}
       receive
         {:response, data} -> data
       end
   end
   def cast(pid, arguments) do
       # runs in the caller context 🐌Alice
       send pid, {:cast, arguments}
   end
   def init() do
      # runs in the server context 🐨Bob
      initial_state = 1
      loop(initial_state)
   end
   def loop(state) do
      # runs in the server context 🐨Bob
      receive command do
         {:call, pid, :get_data} -> 
           # do some work on data here and update state         
           {new_state, response} = {state, state} 
           send pid, {:response, data}
           loop(new_state)
         {:cast, :increment} -> 
           # do some work on data here and update state         
           new_state = state + 1
           loop(new_state)      
      end
   end
end
```

Usage

```elixir
pid = SimpleGenServerMock.start_link()
counter = SimpleGenServerMock.call(pid, :get_data)
IO.puts "Counter: #{counter}
SimpleGenServerMock.cast(pid, :increment)
counter = SimpleGenServerMock.call(pid, :get_data)
IO.puts "Counter: #{counter}
```

