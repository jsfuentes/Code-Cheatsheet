# JSon

```elixir
{:json, "~> 1.2"}
```

```elixir
{status, result} = JSON.encode(list)

json_input = "{\"key\":\"this will be a value\"}"
{status, list} = JSON.decode(json_input)
```

