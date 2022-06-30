# [Tesla](https://hexdocs.pm/tesla/readme.html)

```elixir
defmodule Http do

  use Tesla

  plug Tesla.Middleware.BaseUrl, "https://webhook.site/ab8b7259-feb4-4e62-b8dd-46bb03b614ba"
  plug Tesla.Middleware.FormUrlencoded

  #plug Tesla.Middleware.Headers, [{"header-name", "header-value"}]

  def go do  #Use this function to test whether a Tesla request succeeds without having to repeatedly type the following variables and their values into iex.
    request_body = %{name: "Joel", age: 21}
    path = "/" 
    post(path, request_body)  #Outside of this module, you would need to write Http.post(...)
  end

end
```

### Plugs

```elixir
plug Tesla.Middleware.JSON
```

Converts the Elixir map into a json string with jason and adds `Content-Type: application/json` to headers

```elixir
plug Tesla.Middleware.BaseUrl, "https://api.test.com"
```

Will append to path unless you start with http

```elixir
plug Tesla.Middleware.FormUrlencoded
```

Convert an Elixir map given as the second argument to the `post()` function into form format: `"name=Joel&age=21"`

Adds `Contet-Type: application/x-www-form-urlencoded` header

```elixir
Tesla.Middleware.BasicAuth 
Tesla.Middleware.DigestAuth
```

https://github.com/teamon/tesla#middleware