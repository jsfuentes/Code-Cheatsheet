## Tasks

Extends spawn to provide better error & introspection

Instead of `spawn/1` and `spawn_link/1`, we use `Task.start/1` and `Task.start_link/1` which return `{:ok, pid}` rather than just the PID. This is what enables tasks to be used in supervision trees. Furthermore, `Task` provides convenience functions, like `Task.async/1` and `Task.await/1`, and functionality to ease distribution.

Can easily run without a supervisor for unessential tasks like emails

```elixir
Task.start(fn -> send_email_to_user(user) end) # 🎉
```

## Setup

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

