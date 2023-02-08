# [Tesla](https://hexdocs.pm/tesla/readme.html)

## Simple Request

```elixir
Tesla.get("https://example.com") #no middleware
```

## Creating Modules

```elixir
defmodule OpenAI do
  use Tesla

  plug Tesla.Middleware.BaseUrl, "https://api.openai.com"

  plug Tesla.Middleware.Headers, [
    {"Authorization", "Bearer #{Application.fetch_env!(:react_phoenix, :openai_api)}"},
    {"Content-type", "application/json"}
  ]

  plug Tesla.Middleware.JSON

	#{:ok, %Tesla.Env{status: 200, body: .... }}
  def go do
    request_body = %{name: "Joel", age: 21}
    path = "/" 
    post(path, request_body)
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