# [Set](https://hexdocs.pm/elixir/1.12/MapSet.html)

```elixir
MapSet.new([2]) |> MapSet.put(4) |> MapSet.put(0)
#MapSet<[0, 2, 4]>

MapSet.member?(MapSet.new([1, 2, 3]), 2)
```

Get unique elements from list

```elixir
list |> MapSet.new |> MapSet.to_list
```

