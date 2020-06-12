# HTTP

HTTPoison uses [hackney](https://github.com/benoitc/hackney) to execute HTTP requests instead of ibrowse

```elixir
    {:httpoison, "~> 1.6"}
```

## Usage

Need options rn b/c of latest elixir default change

HTTPoison.start

```elixir
{:ok, response} = HTTPoison.get(url, headers, options)

url = "https://www.googleapis.com/oauth2/v1/userinfo?alt=json&access_token=" <> gaccess_token
options = [ssl: [{:versions, [:"tlsv1.2"]}]]
%HTTPoison.Response{status_code: 200, body: body} = HTTPoison.get!(url, [], options)
profile = Jason.decode!(body)
```

```elixir
iex> HTTPoison.start
iex> HTTPoison.get! "http://httparrot.herokuapp.com/get"
%HTTPoison.Response{
  body: "{\n  \"args\": {},\n  \"headers\": {} ...",
  headers: [{"Connection", "keep-alive"}, {"Server", "Cowboy"},
  {"Date", "Sat, 06 Jun 2015 03:52:13 GMT"}, {"Content-Length", "495"},
  {"Content-Type", "application/json"}, {"Via", "1.1 vegur"}],
  status_code: 200
}
iex> HTTPoison.get! "http://localhost:1"
** (HTTPoison.Error) :econnrefused
iex> HTTPoison.get "http://localhost:1"
{:error, %HTTPoison.Error{id: nil, reason: :econnrefused}}

iex> HTTPoison.post "http://httparrot.herokuapp.com/post", "{\"body\": \"test\"}", [{"Content-Type", "application/json"}]
```

### Pattern Match

```elixir
case HTTPoison.get(url) do
  {:ok, %HTTPoison.Response{status_code: 200, body: body}} ->
    IO.puts body
  {:ok, %HTTPoison.Response{status_code: 404}} ->
    IO.puts "Not found :("
  {:error, %HTTPoison.Error{reason: reason}} ->
    IO.inspect reason
end
```

