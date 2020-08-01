# Plugs

Plugs implement two fts `init` and `call` which takes in a conn and return a conn

## Fetchable Fields

Must fetch them before use, best placed in the router.ex plug list. For example, the `cookies` field uses [`fetch_cookies/2`](https://hexdocs.pm/plug/Plug.Conn.html#fetch_cookies/2).

- `cookies`- the request cookies with the response cookies
- `body_params` - the request body params, populated through a [`Plug.Parsers`](https://hexdocs.pm/plug/Plug.Parsers.html) parser.
- `query_params` - the request query params, populated through [`fetch_query_params/2`](https://hexdocs.pm/plug/Plug.Conn.html#fetch_query_params/2)
- `path_params` - the request path params, populated by routers such as [`Plug.Router`](https://hexdocs.pm/plug/Plug.Router.html)
- `params` - the request params, the result of merging the `:path_params` on top of `:body_params` on top of `:query_params`
- `req_cookies` - the request cookies (without the response ones)

### Functions

| Ft                                                           | Effect                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [assign(conn, key, value)](https://hexdocs.pm/plug/Plug.Conn.html#assign/3) | Assigns a value to a key in the connection.                  |
| [halt(conn)](https://hexdocs.pm/plug/Plug.Conn.html#halt/1)  | Stops the plug pipeline . [See](https://hexdocs.pm/plug/Plug.Builder.html) |
| [put_session(conn, key, value)](https://hexdocs.pm/plug/Plug.Conn.html#put_session/3) |                                                              |
| [put_status(conn, status)](https://hexdocs.pm/plug/Plug.Conn.html#put_status/2) | Return status                                                |
| [send_resp(conn, status, body)](https://hexdocs.pm/plug/Plug.Conn.html#send_resp/3) | Sends a response with the given status and body.             |
|                                                              |                                                              |

### Custom Plug

react_phoenix_web/plugs

```elixir
defmodule ReactPhoenixWeb.IsOrganizer do
  import Plug.Conn
  import Phoenix.Controller

  # alias ReactPhoenixWeb.Router.Helpers

  def init(opts), do: opts

  def call(conn = %{assigns: %{current_user: %{type: "organizer"}}}, _opts), do: conn

  def call(conn, _opts) do
    conn
    |> put_status(401)
    |> text("Unauthorized")
    |> halt()
  end
end
```

some controller

```elixir
defmodule ReactPhoenixWeb.EventController do
  use ReactPhoenixWeb, :controller
  require Logger
  
  plug ReactPhoenixWeb.LoggedIn
       when action in [:post_analytics]

  plug ReactPhoenixWeb.IsOrganizer
       when action in [:index, :create, :update, :delete, :get_analytics]
```



#### Auth Example

Usage `conn.assigns.current_user`

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

	#opts are then passed to every future call
  def call(conn, _opts) do
    user_id = get_session(conn, :user_id)
    user = user_id && Discuss.Accounts.get_user!(user_id)
    assign(conn, :current_user, user) #only available for current connection
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

