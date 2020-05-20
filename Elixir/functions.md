# Functions

Defined by **name** and # of args(**arity**) `hello/1` vs `hello/2`

Instead of early exits/for invalid args use **guards** and param pattern matching

Named Fts must be defined inside module, anon fts can be defined anywhere

### Named Fts

```elixir
defmodule M do
    def transform(myvar, _opts) do #_ means ignore arg
        8 * myvar + 3 #returns last value automatically
    end
    
    #defp for private fts
    defp privateTransform(v, z \\ 1) do  #default value
    	v * 4 + z
    end

		def getcookie(%{cookie: c} = conn, _params) do
    	IO.inspect(conn)
    	IO.puts("Has cookie #{c}")
    end
    
    def getcookie(conn, _params) do
    	IO.puts("No cookie")
    end
end
```

Recursion

```elixir
def factorial(num) do
	if num <= 1 do 
		1
	else 
		result = num * factorial(num - 1)
		result
	end
end
```

Loop?

```elixir
def sum([]), do: 0
def sum([h|t]), do: h + sum(t)

IO.puts("Sum: #{sum([1,2,3])}")
```

```elixir
def loop(0, _), do: nil
def loop(max, min) do
	if(max < min) do
		loop(0, -1)
	else 
		IO.puts "Num: #{max}"
		loop(max - 1, min)
	end
end

myloop(5,1) #=> 5,4,3,2,1
```

Guards

```elixir
def drive(%User{age: age}) when age >= 16 do
  # Code that drives a car
end

drive(User.get("John Doe"))
#=> Fails if the user is under 16
```

```elixir
def print_multiple_times(msg, n) when n <= 1 do
	IO.puts msg
end

def print_multiple_times(msg, n) do
  IO.puts msg
  print_multiple_times(msg, n - 1)
end
```

#### Pipe |>

Output from the left is passed as first arg to ft on right

```elixir
Enum.sum(Enum.filter(Enum.map(1..100_000, &(&1 * 3)), odd?)) 
#becomes
1..100_000 |> Enum.map(&(&1 * 3)) |> Enum.filter(odd?) |> Enum.sum
```

#### Anonymous fts

Defined within a variable scope

**Need a `.` after ft name to call**, `&` can capture Module fts making it anon and also create anon fts

`&List.flatten(&1, &2)` is the same as writing `fn(list, tail) -> List.flatten(list, tail)` end

```elixir
get_sum = fn (x,y) -> x + y end
IO.puts "5 + 5 = #{get_sum.(5,5)}"

get_less = &(&1 - &2)
IO.puts "7 - 6 = #{get_less.(7,6)}"

add_sum = fn #no args notice
	{x, y} -> IO.puts "#{x} + #{y} = {x+y}"
	{x, y, z} -> IO.puts "#{x} + #{y} + #{z} = {x+y+z}"
end
add_sum.({1,2})
add_sum.({1,2,3})
```

