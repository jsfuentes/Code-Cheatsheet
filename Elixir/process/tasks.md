#[Tasks](https://hexdocs.pm/elixir/Task.html)

- Extends spawn to provide better error & introspection
- Meant to execute on task with little communication, like turning seq code into async to compute values/send requests

### Methods Overview

-  `Task.start/1`
-  `Task.start_link/1`
-  `Task.async/1` - expects reply that is always sent (will crash if caller crashes)
-  `Task.await/1`

## Sequential => Concurrent Code

```elixir
task = Task.async(fn -> do_some_work() end)
res = do_some_other_work()
res + Task.await(task)
```

## Adhoc Tasks

Can easily run without a supervisor for unessential tasks like emails

```elixir
Task.start(fn -> send_email_to_user(user) end) # 🎉
```

##### Async requests

```elixir
1..2 |> Task.async_stream(fn(_) -> DailyHelper.createDailyRoom() end) |> Enum.to_list()
#[{:ok, %{..}}, {:ok, %{..}}]
```

## Task Supervisor 

Summary:

- Use [`Task.Supervisor.start_child/2`](https://hexdocs.pm/elixir/1.12/Task.Supervisor.html#start_child/2) to start a fire-and-forget task and you don't care about its results nor about if it completes successfully
- Use [`Task.Supervisor.async/2`](https://hexdocs.pm/elixir/1.12/Task.Supervisor.html#async/2) + [`Task.await/2`](https://hexdocs.pm/elixir/1.12/Task.html#await/2) allows you to execute tasks concurrently and retrieve its result. If the task fails, the caller will also fail
- Use [`Task.Supervisor.async_nolink/2`](https://hexdocs.pm/elixir/1.12/Task.Supervisor.html#async_nolink/2) + [`Task.yield/2`](https://hexdocs.pm/elixir/1.12/Task.html#yield/2) + [`Task.shutdown/2`](https://hexdocs.pm/elixir/1.12/Task.html#shutdown/2) allows you to execute tasks concurrently and retrieve their results or the reason they failed within a given time frame. If the task fails, the caller won't fail: you will receive the error reason either on `yield` or `shutdown`

#### Setup

Application.ex

```elixir
    children = [
      {Task.Supervisor, name: YourApp.AccountSetupSupervisor}
    ]
```

Somewhere in app

```
{:ok, pid} = Task.Supervisor.start_child(ExampleApp.TaskSupervisor, fn -> background_work end)
```

account_setup.ex

Tasks will be run with when that ft

```elixir
defmodule YourApp.AccountSetupSupervisor do
  def set_up_user_account(user) do
    opts = [restart: :transient]

    Task.Supervisor.start_child(__MODULE__, YourApp.CRM, :create_user, [user], opts)
    Task.Supervisor.start_child(__MODULE__, YourApp.Fulfillment, :set_nearest_location, [user], opts)
  end
end
```

Your  CRM sample

```elixir
defmodule YourApp.CRM do

  def create_user(user) do
    crm_data =
      user
      |> fetch_crm_data()
      |> parse()

    user
    |> YourApp.User.crm_changeset(crm_data)
    |> YourApp.Repo.update!()
  end

  defp fetch_crm_data(user) do
    # your code here
  end

  defp parse(data) do
    # you will probably want to parse results for use in a changeset
  end
end
```

