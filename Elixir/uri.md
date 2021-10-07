# URI

```elixir
uri_string =
  base_url
  |> URI.parse()
  |> Map.put(:query, URI.encode_query(params))
  |> URI.to_string()
```

