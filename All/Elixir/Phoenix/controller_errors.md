# Handling Controller Errors

### Return Status

Complete list of status code

https://hexdocs.pm/plug/Plug.Conn.Status.html

```elixir
# 401 Unauthorized
send_resp(conn, 401, '')
send_resp(conn, :unauthorized, '') # same as above
```

If an error is raised during controller, its a 500

#### Development Errors

Phoenix auto creates a nice html page for `raise` errors in dev

dev.exs

```elixir
config :react_phoenix, ReactPhoenixWeb.Endpoint,
  http: [port: 4000],
  debug_errors: false, #to disable for api endpoints
```

In prod, [ErrorView](https://hexdocs.pm/phoenix/1.4.0/views.html#the-errorview) will be used. Ecto.NoResultsError in ecto will be translated to 404, but everything else is usually a 500.

If you return a non conn, will be 500 orrr

### [Fallback](https://hexdocs.pm/phoenix/Phoenix.Controller.html#action_fallback/1)

Is not triggered when an error is raised, only when conn returns an error like in a with statement

Transforms nonconn response to valid conn response

```elixir
defmodule MyController do
  use Phoenix.Controller

  action_fallback MyFallbackController
  
  def show(conn, %{"id" => id}, current_user) do
    with {:ok, post} <- Blog.fetch_post(id),
         :ok <- Authorizer.authorize(current_user, :view, post) do

      render(conn, "show.json", post: post)
    end
  end
end
```

If with fails, it just returns the unmatched value which probably has` {:error, ....}` in it. So in fallback controller

```elixir
defmodule ReactPhoenixWeb.FallbackController do
  @moduledoc """
  Translates controller action results into valid `Plug.Conn` responses.

  See `Phoenix.Controller.action_fallback/1` for more details.
  """
  use ReactPhoenixWeb, :controller

  # This clause handles errors returned by Ecto's insert/update/delete.
  def call(conn, {:error, %Ecto.Changeset{} = changeset}) do
    conn
    |> put_status(:unprocessable_entity)
    |> put_view(ReactPhoenixWeb.ChangesetView)
    |> render("error.json", changeset: changeset)
  end

  # This clause is an example of how to handle resources that cannot be found.
  def call(conn, {:error, :not_found}) do
    conn
    |> put_status(:not_found)
    |> put_view(ReactPhoenixWeb.ErrorView)
    |> render(:"404")
  end
end
```

## ErrorView

