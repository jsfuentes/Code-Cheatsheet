# Workers

Like agents, schedulers can be included in the 

application.ex

```elixir
  def start(_type, _args) do
    # List all child processes to be supervised
    children = [
			# Starts a worker by calling: ReactPhoenix.Worker.start_link(arg)
      {ReactPhoenix.Store.EventState, []},
```

Scheduler.ex

```elixir
# Will send messages with a topic for each user_id
defmodule ReactPhoenixWeb.Scheduler do
  use GenServer
  require Logger

	def start_link(_) do
    GenServer.start_link(__MODULE__, nil, name: __MODULE__)

  def new_user(id) do
    Logger.debug("SCH: NEW_USER #{id}")
    %{topic: topic} = GenServer.call(__MODULE__, {:new_user, id})
    Logger.debug("SCH: AFTER NEW_USER #{topic}")
    send(__MODULE__, :try_schedule)
  end

  def delete_user(id) do
    Logger.debug("SCH: delete_user #{id}")
    GenServer.cast(__MODULE__, {:delete_user, id})
  end

  # GenServer Functions
  def init(_) do
    Logger.debug("SCH: init#{topic}")
    # :timer.send_interval(60 * 1000, :update)
    {:ok, nil}
  end

  def handle_cast({:delete_user, id}, %{topic: topic, users: users}) do
    Logger.debug("SCH: handle_call:delete_user#{id}")
    newUsers = List.keydelete(users, id, 0)
    newState = %{topic: topic, users: newUsers}
    # TODO: Also find and kick out of room other user
    {:noreply, newState}
  end

  def handle_call({:new_user, id}, _, %{topic: topic, users: users}) do
    Logger.debug("SCH: handle_call:new_user#{id}")
    newUsers = [{id, %{}} | users]
    newState = %{topic: topic, users: newUsers}
    {:reply, newState, newState}
  end

  # only one user
  def handle_info(:try_schedule, %{topic: topic, users: [{uid, data}]}),
    do: {:noreply, %{topic: topic, users: [{uid, data}]}}

  def handle_info(:try_schedule, %{topic: topic, users: users}) do
    Logger.debug("SCH: handle_info:try_schedule MULTI USER")
	#.....
    {:noreply, %{topic: topic, users: users}}
  end
end

```

