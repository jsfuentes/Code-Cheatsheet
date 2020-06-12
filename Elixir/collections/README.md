# Collections

Functional so no inplace

## [Enum](https://hexdocs.pm/elixir/Enum.html)

Provies set of algs to enumerate enumeratable types

```elixir
Enum.each list4, fn item ->
	IO.puts item
end
len = Enum.count(l)
```

Map, Reduce, Filter

```elixir
Enum.map([1, 2, 3], fn x -> x * 2 end)
Enum.map(%{1 => 2, 3 => 4}, fn {k, v} -> k * v end)
Enum.map(%{1 => 2, 3 => 4}, fn {k, _} -> k === 3 end)

Enum.reduce(1..3, 0, fn (new, acc) -> new + acc end)

Enum.filter([1,2,3], fn a -> a in [1,3] end)
Enum.filter([1,2,3], fn a -> a not in [1,3] end)
```

Enums are eager so a pipe means an intermediate list is always created

```elixir
1..100_000 |> Enum.map(&(&1 * 3)) |> Enum.filter(odd?) |> Enum.sum
```

Other

```elixir
Enum.sort_by(events, & &1.start_time)
Enum.sort_by(events, & &1.start_time, :desc)
Enum.sort_by(iterable, mapper, sort_ft // Kernel.<=)
Enum.uniq([1,2,2]) #[1,2]
Enum.all?([1,2,3], fn(n) -> rem(n, 2) == 0 end) #false
Enum.any?([1,2,3], fn(n) -> rem(n, 2) == 0 end) #true
Enum.any?([1,2,3], fn(n) -> IO.puts n end) #1\n2\n3\n
```

- .shuffle(enum)
- .member(enum, el)
- .split(enum, count) => returns tuple of two enums with count in first one

### Comprehension

```elixir
for n <- [1, 2, 3, 4], do: n * n
for n <- 1..4, do: n * n
values = [good: 1, good: 2, bad: 3, good: 4]
for {:good, n} <- values, do: n * n #[1, 4, 16]
```

### Streams

Useful for large collections

Streams are lazy build series of computations that only becomes something when passed to Enum

```elixir
1..100_000 |> Stream.map(&(&1 * 3)) |> Stream.filter(odd?) #Stream<[enum: 1..100000, funs: [...]]>
```

Stream also has fts to create streams

```elixir
Stream.cycle([1, 2, 3]) # cycles infinitely
Enum.take(stream, 10) #[1, 2, 3, 1, 2, 3, 1, 2, 3, 1]

Stream.unfold("hełło", &String.next_codepoint/1) #generate from initial val
stream = File.stream!("path/to/file")
Enum.take(stream, 10) #first 10 lines
```

