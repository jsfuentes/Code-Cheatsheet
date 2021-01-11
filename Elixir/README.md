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
-  `==`, `!=`, `===`(doesn't count integers and floats as equal, but **works at comparing native objects! [1,2] === [1,2]**), `!==`, `<=`, `>=`, `<` and `>`
-  Use pin operator `^` to pattern match against variables cur value: `x = 1 ^x = 2` => Error no match 1 = 2 ( apparently also used in queries for [type coercion](https://dev.to/lasseebert/til-ecto-s-pin-is-coercing-19fh))
-  `"a"` is UTF-8 encoded binary while `'a'` is charlist 

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
		1
	end
end
```

Doesn't actually need main or anything

#### IO

Print internal representation

```elixir
IO.inspect String.split(longer_str, " ") 
IO.write "No newline"
a = "hi"
IO.puts "Puts with newline #{a}" 
IO.puts(:stderr, "error bb")
x = IO.gets("yes or no?") #prompts user and return string with newline

(1..10)
|> IO.inspect #returns param for easy pipe usage
|> Enum.map(fn x -> x * 2 end)
```

`IO.inspect [97, 98] ` => [a,b]

`IO.inspect [97, 98], char_lists: :as_lists` => [97, 98]

### Branches

```elixir
age = 16
if age >= 18 do
	IO.puts "Can Vote"
else #no else if
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
cond do #checks list of conditions
	x -> IO.puts "You can vote"
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

#### With

```elixir
with {:ok, user} <- create_user(user_params),
     {:ok, email} <- Mailer.compose_email(user) do
  {:ok, Mailer.send_email}
else
  {:error, _reason} ->
    handle_error
end

with user_id when not is_nil(user_id) <- get_session(conn, :user_id),
       user when not is_nil(user) <- Repo.get(User, user_id)
  do
    assign(conn, :current_user, user)
  else
    _ ->
      conn
      |> Controller.put_flash(:error, "You have to sign in to access this page.")
      |> Controller.redirect(to: "/sign_in_links/new")
      |> halt
  end
```

In the code snippet above we've rewrite nested `case` clauses with `with`. Within `with` we invoke some functions (either anonymous or named) and pattern match on their outputs. If all matched, `with` return `do` block result, or `else` block result otherwise.

We can omit `else` so `with` will return either `do` block result or the first fail result.

### Type Converstion

```elixir
Integer.to_string(123) #"123"
```

