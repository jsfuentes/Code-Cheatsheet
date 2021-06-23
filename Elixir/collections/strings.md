# [String](https://hexdocs.pm/elixir/String.html#summary)

```elixir
"hello"
"string" <> "concat"

x = 123
x <> "hi" #error
"#{x}hi" #123hi
```



String.reverse(str)

String.upcase(str)

String.downcase(str)

String.capitalize(str)

String.starts_with?(str)

String.contains?(str, "search_str")

String.first(str)

String.at(str, index)

String.slice(str, start_index, end_index)

String.split("foo bar", "")

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
Atom.to_string(:foo) 
```

_Atoms are not garbage collected, so never convert user input to atoms_

