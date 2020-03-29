#### Tuple

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

#### Lists(linked)

```elixir
list1 = [1,2,3]
list2= [4,5,6]
list3 = list1 ++ list2
list4 = list3 -- list1
IO.puts 6 in list4
[head | tail] = list3
display_list(List.delete(list4, 1))
display_list(List.delete_at(list4, 1))
display_list(List.insert_at(list4, 2))
IO.puts List.first(list4) //?
IO.puts List.last(words) //?

Enum.each list4, fn item ->
	IO.puts item
end
#check if even list
Enum.all?([1,2,3], fn(n) -> rem(n, 2) == 0 end) #false
Enum.any?([1,2,3], fn(n) -> rem(n, 2) == 0 end) #true
Enum.any?([1,2,3], fn(n) -> IO.puts n end) #1\n2\n3\n
dbl_list = Enum.map([1,2,3], fn(n) -> n * 2 end)
sum_val = Enum.reduce([1,2,3], fn(n, sum) -> n + sum end)
Enum.uniq([1,2,2]) #[1,2]
```

List Comprehension

```elixir
dbl_list = for n <- [1,2,3], do: n * 2
IO.inspect dbl_list
even_list = for n <- [1,2,3,4], rem(n,2) == 0, do: n #filters on condition rem...
```

Recursion 

```elixir
def display_list([word | words]) do
	IO.puts word
	display_list(words)
end

def display_list([]), do: nil
```

#### Map

```elixir
capitals = %{"Alabama" => "Montgomery",
	"Alaska" => "Juneau", "Arizona" => "Phoenix"}
IO.puts "Capital of Alaska is #{capitals["Alaska"]}"

capitals = %{alabama: "Montgomery",
	alaska: "Juneau", arizona: "Phoenix"}
IO.puts "Capital of Alabama is #{capitals2.arizona}"
capitals3 = Dict.put_new(capitals, "Arkansas", "Little Rock")
```

Pattern matching

```elixir
[length, width] = [20, 40]
[ ,[ , a]] = [20, [30, 40]]
```

