# Collections

Functional so no inplace

## [Enum](https://hexdocs.pm/elixir/Enum.html)

Provies set of algs to enumerate enumeratable types

Loop, length

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
#[2, 12]
Enum.map(%{1 => 2, 3 => 4}, fn {k, _} -> k === 3 end) #[false, true]
%{monday: 28, tuesday: 29, wednesday: 29}
|> Enum.map(fn ({d, t}) -> {d, t * 1.8 + 32} end)
|> Enum.into(%{})

Enum.reduce(1..3, 0, fn (new, acc) -> new + acc end)
Enum.reduce([%{a: 1}, %{b: 2}], %{}, &Map.merge/2)

Enum.filter([1,2,3], fn a -> a in [1,3] end) #[1,3]
Enum.filter([1,2,3], fn a -> a not in [1,3] end)
Enum.filter(%{a: 1, b: 4}, fn {x, y} -> y === 1 end)
#[a: 1]

#returns first val that fn returns truthy val or default
Enum.find(enum, default, fn)
Enum.find([1,2], 3, fn x -> x > 3 end) # 3
```

Enums are eager so a pipe means an intermediate list is always created

```elixir
1..100_000 |> Enum.map(&(&1 * 3)) |> Enum.filter(odd?) |> Enum.sum
```

Other

```elixir
Enum.uniq([1,2,2]) #[1,2]
Enum.all?([1,2,3], fn(n) -> rem(n, 2) == 0 end) #false
Enum.any?([1,2,3], fn(n) -> rem(n, 2) == 0 end) #true
Enum.any?([1,2,3], fn(n) -> IO.puts n end) #1\n2\n3\n
Enum.random(1..3) #random element from list
Enum.join(["StringA", "StringB"], " ")
```

- .shuffle(enum)
- .member(enum, el)
- .split(enum, count) => returns tuple of two enums with count in first one

#### Sort

```elixir
Enum.sort([2, 3, 1], :asc) #<=/2 sorting, [1,2,3]
Enum.sort([2, 3, 1], :desc) #>=/2 sorting, [3,2,1]
Enum.sort_by(iterable, mapper, sort_ft // Kernel.<=)
```

##### Sorting Dates

Do not use <= or >= when using structs/dates

Passing a module, uses that module's `compare/2` 

```elixir
Enum.sort(dates, Date)
Enum.sort(dates, {:asc, Date})
```

### Comprehension

```elixir
for n <- [1, 2, 3, 4], do: n * n
for n <- 1..4, do: n * n # inclusive of both sides
values = [good: 1, good: 2, bad: 3, good: 4]
for {:good, n} <- values, do: n * n #[1, 4, 16]
```

## Parallelize

#### Tasks

```elixir
1..2 |> Task.async_stream(fn(_) -> DailyHelper.createDailyRoom() end) |> Enum.to_list()
#[{:ok, %{..}}, {:ok, %{..}}]
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

