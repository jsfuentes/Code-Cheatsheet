# Controllers

lib/hello_web/controllers/hello_controller.ex

```elixir
defmodule HelloWeb.HelloController do
  use HelloWeb, :controller
  #import an Auth Plugin ft
  import Hello.Auth, only: [logged_in_user: 2]
  #pass through plug with a guard(like middleware)
  plug :logged_in_user when action not in [:new, :create]


  def index(conn, _params) do #ACTION
    render(conn, "index.html") 
    #find and render index.html.eex in lib/hello_web/templates/hello (named after controller)
  end
  
  def show(conn, %{"messenger" => messenger}) do
    render(conn, "show.html", messenger: messenger)
    #gets :messenger from /hello/:messenger route
  end
end
```

### Actions

All actions take two args:

- `conn`: a struct which holds data about requests
- `params`: request params

## API Stuff

web/controllers/user_controller

```elixir
 defmodule ApiExample.UserController do
  use ApiExample.Web, :controller
  def index(conn, _params) do
    users = [
      %{name: "Joe",
        email: "joe@example.com",
        password: "topsecret",
        stooge: "moe"},
      %{name: "Anne",
        email: "anne@example.com",
        password: "guessme",
        stooge: "larry"},
      %{name: "Franklin",
        email: "franklin@example.com",
        password: "guessme",
        stooge: "curly"},
    ]
    json conn, users
  end
end
```

Phoneix actualmagically parse the post body and puts it in params