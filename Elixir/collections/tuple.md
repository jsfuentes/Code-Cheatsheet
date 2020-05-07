# Tuples

Can hold any value, but not for enumeration

Arrays continuous in memory, but new ones require new continuous memory. Contents aren't copied, contents are shared

```elixir
my_stats = {175, 5.25, :Derek}
IO.puts "Tuple ${is_tuple(my_stats)}"
my_stats2 = Tuple.append(my_stats, 42)
IO.puts "Age: #{elem(my_stats2, 3)}"
IO.puts "Size: #{tuple_size(my_stats2, 3)}"
my_stats3 = Tuple.delete_at(my_stats2, 0)
my_stats4 = Tuple.insert_at(my_stats3, 0, 1974)
many_zeroes = Tuple.duplicate(0, 5)

{weight, height, name} = {175, 6.25, "Derek"}
IO.puts "Weight: #{weight}"
```

#### 