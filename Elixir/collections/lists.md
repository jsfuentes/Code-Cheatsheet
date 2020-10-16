# Lists(linked)

```elixir
list1 = [1,2,3]
list2= [4,5,6]
list3 = list1 ++ list2
list4 = list3 -- list1

6 in list4

[head | tail] = list3
display_list(List.delete(list4, 1))
display_list(List.delete_at(list4, 1))
display_list(List.insert_at(list4, 2))

List.first(list4) //?
List.last(words) //?
```

List Comprehension

```elixir
dbl_list = for n <- [1,2,3], do: n * 2
IO.inspect dbl_list
even_list = for n <- [1,2,3,4], rem(n,2) == 0, do: n #filters on condition rem...

cards = for value <- values, suit <- suits do
	"#{value} of #{suit}"
end #[10 of hearts, 11 of hearts, ...]
```

Recursion 

```elixir
def display_list([word | words]) do
	IO.puts word
	display_list(words)
end

def display_list([]), do: nil
```

