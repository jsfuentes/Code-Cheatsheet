# Functions

Functions defined by name and # of args(arity)

Functions return last value automatically

Anonyomus functions with some crazy shorthand

```elixir
get_sum = fn (x,y) -> x + y end
IO.puts "5 + 5 = #{get_sum.(5,5)}"

get_less = &(&1 - &2)
IO.puts "7 - 6 = #{get_less.(7,6)}"

add_sum = fn
	{x, y} -> IO.puts "#{x} + #{y} = {x+y}"
	{x, y, z} -> IO.puts "#{x} + #{y} + #{z} = {x+y+z}"
end
add_sum.({1,2})
add_sum.({1,2,3})
```

Default values

```elixir
IO.puts do_it()
def do_it(x \\ 1, y\\1) do
	x + y
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
def sum([h|t]), do: h + s um(t)

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

### 