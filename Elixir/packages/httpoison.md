# [HTTPoison](https://hexdocs.pm/httpoison/HTTPoison.html)

`mix deps.update hackney`  for **quick fix**

HTTPoison uses [hackney](https://github.com/benoitc/hackney) to execute HTTP requests instead of ibrowse

```elixir
    {:httpoison, "~> 1.6"}
```

## Usage

#### Get

```elixir
{:ok, response} = HTTPoison.get(url, headers, options)

url = "https://www.googleapis.com/oauth2/v1/userinfo?alt=json&access_token=" <> gaccess_token

%HTTPoison.Response{status_code: 200, body: body} = HTTPoison.get!(url, [])
profile = Jason.decode!(body)
```

```elixir
iex> HTTPoison.start
iex> HTTPoison.get! "http://httparrot.herokuapp.com/get"

iex> HTTPoison.get! "http://localhost:1"
** (HTTPoison.Error) :econnrefused
iex> HTTPoison.get "http://localhost:1"
{:error, %HTTPoison.Error{id: nil, reason: :econnrefused}}
```

#### Post

```elixir
rawPayload = %{privacy: "public"}
payload = Jason.encode!(rawPayload)
url = "https://api.daily.co/v1/rooms"
headers = [
Accept: "Application/json; Charset=utf-8",
"Content-Type": "Application/json; charset=utf-8",
Authorization: "Bearer #{Application.fetch_env!(:react_phoenix, :daily_api)}"
]

case HTTPoison.post(url, payload, headers) do
	{:ok, %HTTPoison.Response{status_code: 200, body: body}} ->
		Logger.debug("CREATED DAILY ROOM")
		Jason.decode!(body)

	{:ok, %HTTPoison.Response{status_code: 400, body: body}} ->
		Logger.error("Problem creating room")
		IO.inspect(body)
		Sentry.capture_message("Create DailyRoom fails",
extra: %{body: body})
		%{}
	{:error, %HTTPoison.Error{reason: reason}} ->
		Logger.debug("Daily room creation failed for #{reason}")
		%{}
end
```

iex

```elixir
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

