# Elixir

Functional highly scalable language for realtime data built on Erlang VM allowing usage of Erlang libs/functions

Ruby-like functional programming

Runs inside lightweight threads(called processes) communicating via messages even if on different machines so legit horizontal scale

- Hex package manager

## Basic

- Double and triple equals like javascript(type conversion vs no type conversion)
- if else, ruby unless, switch => case, long if else can be cond similar to Ocaml
- Immutable, dynamically typed values
- Like erlang, function returns the last value
- Can't do for (int ....) b/c immutable, must use recursion
-  `=` operator is actually called *the match operator*
- `someFunction/2` means someFunction with two args as functions unique by name & arg count

test.exs

```elixir
#comments
defmodule M do
	def main do
		do_stuff()
	end
	
	def do_stuff do
		my_str = "My Sentence"
		IO.puts "Length: #{String.length(my_str)}"
		IO.puts not true
	end
end
```

Doesn't actually need main or anything

#### IO

Print internal representation

```elixir
IO.inspect String.split(longer_str, " ") 
IO.write "No newline"
IO.puts "Puts with newline"
```

`IO.inspect [97, 98] ` => [a,b]

`IO.inspect [97, 98], char_lists: :as_lists` => [97, 98]

#### Strings

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

#### Math

All ops normal, except `/` always returns float

div(5, 4) is integer division => 1

rem(5, 4) is modulo => 1

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

 `or`, `and`, `not`  short circuit

 `==`, `!=`, `===`, `!==`, `<=`, `>=`, `<` and `>`

### Branches

```elixir
age = 16
if age >= 18 do
	IO.puts "Can Vote"
else 
	IO.puts "Can't Vote" 
end

unless age === 18 do 
	IO.puts "You're not 18"
else 
	IO.puts "You are 18"
end
```

Conditional Matching, goes to first match

```elixir
cond do 
	age >= 18 -> IO.puts "You can vote"
	age >= 16 -> IO.puts "You can drive"
	age >= 14 -> IO.puts "You can wait"
	true -> IO.puts "Default"
end
```

switch

```elixir
case 2 do 
	1 -> IO.puts "Entered 1"
	2-> IO.puts "Entered 2"
	_ -> IO.puts "Default"
end
```

Trenary op

```elixir
canVote = if age > 18, do: "Can Vote", else: "Can't Vote"
```

#### 