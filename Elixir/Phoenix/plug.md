# Adding Plugs

Takes in conn and return conn

router.ex

```elixir
  pipeline :browser do
    plug :accepts, ["html"]
    plug :fetch_session
    plug :fetch_flash
    plug :protect_from_forgery
    plug :put_secure_browser_headers
    plug Discuss.Auth
  end
```

lib/discuss_web/plugs/auth.ex

```elixir
defmodule Discuss.Auth do
  import Plug.Conn
  import Phoenix.Controller
  alias DiscussWeb.Router.Helpers

  def init(opts), do: opts

  def call(conn, _opts) do
    user_id = get_session(conn, :user_id)
    user = user_id && Discuss.Accounts.get_user!(user_id)
    assign(conn, :current_user, user)
  end

  def logged_in_user(conn = %{assigns: %{current_user: %{}}}, _), do: conn

  def logged_in_user(conn, _opts) do
    conn 
    |> put_flash(:error, "You must be logged in to access that page")
    |> redirect(to: Helpers.page_path(conn, :index))
    |> halt()
  end
end
```

app.html.eex

```html
User ID: <%= @current_user.id %>
```

