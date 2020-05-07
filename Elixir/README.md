# Elixir

Functional highly scalable language for realtime data built on Erlang VM allowing usage of Erlang libs/functions like OTP. 

Ruby on Rails-like immutable, **dynamically typed**, **functional language**

Runs inside lightweight threads(called **processes**) communicating via **messages** even if on different machines so legit horizontal scale(Erlang VM handles multi-machine, can also implement with Redis)

Elixir uses **supervisers** and processes fail fast. If there is an error, restart in proper/known state

- **Hex** package manager
- Elixir used by Brex, Tandem, Pagerduty
- Inline code tests
- Pure Functional
  - no class with internal state, but modules that init or transform an input state and return new state
  - Not indexable list, but recursive head rest pattern matching
- To dealing with state across processes, use Erlang Term Storage([ETS](http://www.erlang.org/doc/man/ets.html)) or processes like **Agents, Genserver**  

## Basic

- Double and triple equals like javascript(type conversion vs no type conversion)
- `if age === 18 do [.] else [.] end`, ruby unless, switch => case, long if else can be cond similar to Ocaml
- Like erlang, function returns the last value
- Can't do for (int ....) b/c immutable, must use recursion
-  `=` operator is actually called *the match operator*
- `someFunction/2` means someFunction with two args as functions unique by name & arg count(arity)
-  `or`, `and`, `not`  and can short circuit
-  `==`, `!=`, `===`, `!==`, `<=`, `>=`, `<` and `>`

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
IO.puts(:stderr, "error bb")
x = IO.gets("yes or no?") #prompts user and return string with newline

(1..10)
|> IO.inspect #returns param for easy pipe usage
|> Enum.map(fn x -> x * 2 end)
```

`IO.inspect [97, 98] ` => [a,b]

`IO.inspect [97, 98], char_lists: :as_lists` => [97, 98]

#### Math

All ops normal, except `/` always returns float

div(5, 4) is integer division => 1

rem(5, 4) is modulo => 1

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
	2 -> IO.puts "Entered 2"
	_ -> IO.puts "Default"
end
```

Trenary op

```elixir
canvote = if age > 18, do: "Can Vote", else: "Can't Vote"
```

#### 