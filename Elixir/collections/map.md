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

#### Get

```elixir
map = %{a: 1, b: 2}
Map.get(“key”) || Map.get(:key) #Atom and String

#Use the atom or string
Map.get(map, :c) #nil
Map.get(map, :c, 3) #3
Map.fetch(map, :a) #:error
Map.fetch(map, :c) #{:ok, 1}

map[:b] #atom key
map.b #atom key
map["b"] # String keys

#For dynamic maps
map["non_existing_key"] #nil
map.non_existing_key #Key Error
```

#### Setting

```elixir
Map.put(map, :a, 2)

#for complex nested puts
put_in(deep_map, [:key1, :key2], "key2val")
```

Pattern matching

```elixir
[length, width] = [20, 40]
[ ,[ , a]] = [20, [30, 40]]
x = %{:a => 1, "b" => 2, [:c, :e, :e] => 3}
%{a: a} = x # ATOM MATCHING
%{"b" => b} = x # STRING MATCHING
def hasState?(%{state: _}), do: true
```

#### Other

```elixir
Map.pop(%{a: 1}, :a) #{1, %{}}
Map.pop(%{a: 1}, :b, 3) #default 3: {3, %{a: 1}}
```

Pipe Merging

```elixir
x = %{a: 1, b: 2}
%{x | a: 3} #%{a: 3, b: 2}
%{x | c: 5} #** (KeyError) key :c not found
```

