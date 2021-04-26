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

## Task Supervisor Setup

Application.ex

```elixir
    children = [
      {Task.Supervisor, name: YourApp.AccountSetupSupervisor}
    ]
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

