# Session

Builtin to Phoenix, session_opts defined in `endpoint.ex`

You can put and get things from the session then pass it into the render or I guess return it on api call

- put_session(conn, key, value)
- configure_session(conn, renew: true)
- configure_session(conn, drop: true)
- fetch_session(conn, opts \\\\ [])
- get_session(conn) => all OR get_session(conn, key)

router.ex

```elixir
#...
    get "/login", SessionController, :new
    get "/logout", SessionController, :delete
    resources "/sessions", SessionController, only: [:new, :create, :delete], singleton: true
#...
```

controllers/session_controller.ex

```elixir
defmodule DiscussWeb.SessionController do
  use DiscussWeb, :controller

  alias Discuss.Accounts

  def new(conn, _) do
    render(conn, "new.html")
  end

  def delete(conn, _) do
    conn
    |> configure_session(drop: true)
    |> put_flash(:success, "Successfully signed out")
    |> redirect(to: "/")
  end

  def create(conn, %{"user" => %{"email" => email, "password" => password}}) do
    case Accounts.authenticate_by_email_password(email, password) do #write this ft in Accounts
      {:ok, user} ->
        conn
        |> put_flash(:info, "Welcome back!")
        |> put_session(:user_id, user.id) #Use an Auth Plug to lookup user
        |> configure_session(renew: true)
        |> redirect(to: "/")
      {:error, :unauthorized} ->
        conn
        |> put_flash(:info, "Bad email/password")
        |> redirect(to: Routes.session_path(conn, :new))
      {:error, :not_found} ->
        conn
        |> put_flash(:info, "Account not found!")
        |> redirect(to: Routes.session_path(conn, :new))
    end
  end
end
```

### Plug

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

User_controller.ex

```elixir
defmodule DiscussWeb.UserController do
  use DiscussWeb, :controller

  alias Discuss.Accounts
  alias Discuss.Accounts.User
  import Discuss.Auth, only: [logged_in_user: 2]
  plug :logged_in_user when action not in [:new, :create]
```

app.html.eex

```html
User ID: <%= @current_user && @current_user.id %>
```

