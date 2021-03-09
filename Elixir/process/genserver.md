# GenServer (Generic Server)

- Great for scheduled/cron jobs
- Start seperate process that holds some state, changes its state based on **calls**(sync expecting response) or **casts**(async, no resp) 
- Can recieve other/more messages than agent with handle_info
- GenServer is a single process, so best to minimize server work and only handle scheduling, use Task delegation, or offload most work to client caller

react_phoenix_web/simplegen.ex

```elixir
defmodule ReactPhoenixWeb.SimpleGen do
  use GenServer
  @interval 1_000

	# Runs in Caller Context 🐌Alice
  def start_link(arg1) do
    GenServer.start_link(__MODULE__, arg1)
  end
  
  def increment(count) do
    GenServer.cast(__MODULE__, {:increment, count})
  end
  
  # Runs in Single Server Context 🐨Bob
  def init(arg1) do 
    # start_link calls this
    Process.send_after(self(), :work, @interval)
    {:ok, arg1}
  end
  
  def handle_info(:work, state) do
  	# send/send_after within the server calls this
    Process.send_after(self(), :increment, @interval)
    {:noreply, state}
  end
  
  def handle_call(:get_data, _from, state) do
  	resp = state
    {:reply, resp, state}
  end
  
  def handle_cast({:increment, count}, state) do
    {:noreply, state+count}
  end
end
```

Add to *application.ex* to supervise and init on startup

```elixir
	def start(_type, _args) do
    # List all child processes to be supervised
    children = [
    	#....
      {ReactPhoenixWeb.SimpleGen, 1}
    ]
		#....
```

Then just call with `ReactPhoenixWeb.SimpleGen.increment(5)`

### Raw Examples

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

