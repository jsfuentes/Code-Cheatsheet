# Ueberauth

Oauth Callbacks

```elixir
      {:ueberauth, "~> 0.6"},
      {:ueberauth_google, "~> 0.8"}
```

### Setup

Config/config.exs

```elixir
config :ueberauth, Ueberauth,
  providers: [
    google: {Ueberauth.Strategy.Google, []}
  ]
config :ueberauth, Ueberauth.Strategy.Google.OAuth,
  client_id: "[some_id].apps.googleusercontent.com",
  client_secret: "[some_secret]"
```

router.ex

```elixir
  scope "/auth", ReactPhoenixWeb do
    pipe_through :browser

    get "/:provider", AuthController, :request
    get "/:provider/callback", AuthController, :callback
    post "/:provider/callback", AuthController, :callback
  end
```

controllers/auth_controller.ex

```elixir
defmodule ReactPhoenixWeb.AuthController do
  use ReactPhoenixWeb, :controller
  plug Ueberauth
  alias Ueberauth.Strategy.Helpers
  alias ReactPhoenix.Accounts
  
  def callback(%{assigns: %{ueberauth_failure: _fails}} = conn, _params) do
    IO.puts "Failed uberauth"
    conn
    |> put_flash(:error, "Failed to authenticate.")
    |> redirect(to: "/")
  end

  def callback(%{assigns: %{ueberauth_auth: auth}} = conn, _params) do 
    IO.puts "Got uberauth"
    IO.inspect auth 
    conn 
    |> put_flash(:info, "Successfully authenticated!")
    |> redirect(to: "/")
  end

  def request(conn, _params) do
    render(conn, "request.html", callback_url: Helpers.callback_url(conn))
  end
end
```



