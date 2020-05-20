#  Map

#### Creation

Atoms and strings are DIFFERENT keys with different matching and creation syntax 

```elixir
# String Syntax
capitals = %{"Alabama" => "Montgomery",
	"Alaska" => "Juneau", "Arizona" => "Phoenix"}
# Atom Syntax
capitals2 = %{alabama: "Montgomery",
	alaska: "Juneau", arizona: "Phoenix"}
```

#### Get/Set

```elixir
map = %{a: 1, b: 2}
Map.get(“key”) || Map.get(:key) #Atom and String

Map.get(map, :c) #nil
Map.get(map, :c, 3) #3
Map.fetch(map, :a) #:error
Map.fetch(map, :c) #{:ok, 1}
#!Must be an atom not a string!, good for structs
map[:b]
map.b
#More for dynamic maps
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
x = %{:a => 1, "b" => 2, [:c, :e, :e] => 3}
%{a: a} = x # ATOM MATCHING
%{"b" => b} = x # STRING MATCHING
```

#### Other

```elixir
Map.pop(%{a: 1}, :a) #{1, %{}}
Map.pop(%{a: 1}, :b, 3) #default 3: {3, %{a: 1}}
```