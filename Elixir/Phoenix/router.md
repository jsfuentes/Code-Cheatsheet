# Router

[`mix phx.routes`](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.Routes.html)

lib/eServer_web/router.ex

```elixir
defmodule EServerWeb.Router do
  use EServerWeb, :router #make route fts available here

  pipeline :browser do #middleware
    plug :accepts, ["html"]
    plug :fetch_session
    plug :fetch_flash
    plug :protect_from_forgery
    plug :put_secure_browser_headers
  end

  pipeline :api do
    plug :accepts, ["json"]
  end

  scope "/", EServerWeb do
    pipe_through :browser

		#first clause to match
    get "/", PageController, :index
    get "/hello", HelloController, :index
  	get "/hello/:messenger", HelloController, :show
  	resources "/users", UserController
  end

	forward "/jobs", BackgroundJob.Plug
  # Other scopes may use custom stacks.
  # scope "/api", EServerWeb do
  #   pipe_through :api
  # end
end
```

## Adding Routes

In the scope, its http-verb, Controller, and function in that controller

```elixir
get "/hello", HelloController, :index
```

Then add a controller and view

```elixir
resources "/users", UserController
```

Expands out to

user_path  GET     /users                HelloWeb.UserController :index
user_path  GET     /users/:id/edit  HelloWeb.UserController :edit
user_path  GET     /users/new       HelloWeb.UserController :new
user_path  GET     /users/:id          HelloWeb.UserController :show
user_path  POST    /users              HelloWeb.UserController :create
user_path  PATCH   /users/:id       HelloWeb.UserController :update
                    PUT     /users/:id         HelloWeb.UserController :update
user_path  DELETE  /users/:id       HelloWeb.UserController :delete

```elixir
resources "/posts", PostController, only: [:index, :show]
```

### More

get is actually a Phoenix macro that is one clause of a match for HTTP get request