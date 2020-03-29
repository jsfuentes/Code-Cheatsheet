### Exception Handling

```elixir
err = try do
	5/0
rescue
	ArithmeticError -> "Can't Divide by Zero"
end
IO.puts err
```

