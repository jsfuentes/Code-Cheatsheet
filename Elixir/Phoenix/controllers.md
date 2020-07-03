# Controllers

See **plug** for more info since controllers are plugs

External data uses string keys, internal data uses atoms

### Actions

All actions take two args:

- `conn`: a struct which holds data about requests
- `params`: request params(seems to everything like post body, query params, and more), Map with **string keys** 

Return values with `json/2`,  `text/2`, , and `html/2` 

To let Phoenix views build resp, use `render/3`

lib/hello_web/controllers/hello_controller.ex

```elixir
defmodule HelloWeb.HelloController do
  use HelloWeb, :controller
  import Hello.Auth, only: [logged_in_user: 2]
  #pass through plug with a guard(like middleware)
  plug :logged_in_user when action not in [:new, :create]
  
  #params are combo of /m/:messenger and query params
  def show(conn, %{"messenger" => messenger}) do
    #gets :messenger from /hello/:messenger route
    #render(conn, "show.html", messenger: messenger) ORRRR
    conn
    |> assign(:messenger, messenger)
    |> render("show.html")
    #find and render show.html.eex in lib/hello_web/templates/hello (named after controller)
  end
  
  def redirect(conn, _params) do
  	conn 
  	|> put_flash(:info, "Redirecting")
  	|> redirect(to: "/redirect_test")
  	#  	|> redirect(external: "google.com")
  end
  
  def get(conn, _params) do
    conn
    |> put_status(401)
    |> json(%{user: 1})
  end
end
```
