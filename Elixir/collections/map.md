# Map

#### Creation

```elixir
capitals = %{"Alabama" => "Montgomery",
	"Alaska" => "Juneau", "Arizona" => "Phoenix"}
IO.puts "Capital of Alaska is #{capitals["Alaska"]}"

capitals2 = %{alabama: "Montgomery",
	alaska: "Juneau", arizona: "Phoenix"}
```

#### Get/Set

```elixir
map = %{a: 1, b: 2}
Map.fetch(map, :a) {:ok, 1}
#Use for dynamic maps
map[:b]
map.b
#Use for static maps like structs
map["non_existing_key"] #nil
map.non_existing_key #Key Error
```

```elixir
Map.put(map, :a, 2)
```

Pattern matching

```elixir
[length, width] = [20, 40]
[ ,[ , a]] = [20, [30, 40]]
%{a: a} = %{:a => 1, "b" => 2, [:c, :e, :e] => 3} #a= 1
```

#### Other

-`.pop(map, key, default \\ nil)`

-`.pop!(map, key)`