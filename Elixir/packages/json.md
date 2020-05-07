## Jason

```elixir
      {:jason, "~> 1.2"}
```

## Usage

```elixir
Jason.encode!(%{"age" => 44, "name" => "Steve Irwin", "nationality" => "Australian"})
#"{\"age\":44,\"name\":\"Steve Irwin\",\"nationality\":\"Australian\"}"

Jason.decode!(~s({"age":44,"name":"Steve Irwin","nationality":"Australian"}))
#%{"age" => 44, "name" => "Steve Irwin", "nationality" => "Australian"}
```

### Worse JSON

```elixir
{:json, "~> 1.2"}
```

#### Usage

```elixir
{status, result} = JSON.encode(list)

json_input = "{\"key\":\"this will be a value\"}"
{status, list} = JSON.decode(json_input)
```

