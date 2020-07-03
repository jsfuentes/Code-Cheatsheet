# String

```Elixir
defmodule M do
  def main do
	  do_stuff()
  end

  def do_stuff do
    my_str = "My Sentence"
    IO.puts "Length: #{String.length(my_str)}"
    longer_str = my_str <> " " <> "is longer"
    IO.puts "My ? #{String.contains?(my_str, "My")}"
    IO.puts "First : #{String.first(my_str)}"
    IO.puts "Index 4 ? #{String.at(my_str, 4)}"
    IO.puts "Substring : #{String.slice(my_str, 3, 8)}"
    4 * 10 |> IO.puts
  end
end
```

String.reverse(str)

String.upcase(str)

String.downcase(str)

String.capitalize(str)

### Atoms

An atom is a constant whose value is its own name

`true`, `false`, and `nil` are atoms, but can skip `:`



```elixir
:apple
:ok != :error
:true == true
is_atom(false) # => true
true and true
false or not true
1 and true # => raises exception
```

_Atoms are not garbage collected, so never convert user input to atoms_
