# OTP

 (Open Telecom Platform) is a collection of framework/lib/tools written in Erlang

Horrible error messaging

## Observer

```
iex(1)> observer.start()
```

# [Erlang Term Storage (ETS)](https://elixirschool.com/en/lessons/specifics/ets/)

- [Docs](http://erlang.org/doc/man/ets.html)

In-memory store key value for elixir and erlang

\>10x Faster than redis according [to](https://github.com/minhajuddin/redis_vs_ets_showdown)

- Created and owned by individual processes(destroyed on exit), so back with GenServer and now any process can access, no bottleneck
-  Only limit is server memory.
- Because multiple can access at the same time unlike message based agents, operations must be atomic (ft for something like counter updating)
  - Concurrent reads with serial writes is a common ETS pattern

### Applications of ETS

- persisent shared state(tzdata, )
- ephemeral shared state(cache, rate limiter)
- IPC

### Usage

```elixir
tab = :ets.new(:my_table, [:set]) #=> 8211

:ets.insert(tab, {:key1, "value1"}) #=> true

:ets.lookup(tab, :key1) #=> [key1: "value1"]
```

#### Advanced

```elixir
:ets.tab2list(:rate_limiter_requests) #[[key1: "value1"]]
```

http://erlang.org/doc/man/disk_log.html

### [Disk Based ETS(DETS)](https://erlang.org/doc/man//dets.html)

APIS are interchangeable except

-  how tables are created with named table default
-  `:dets` vs `:ets` and fewer features
- Slower cuz disk

```elixir
{:ok, table} = :dets.open_file(:disk_storage, [type: :set]) #{:ok, :disk_storage}
:dets.open_file(:file_table, [{:file, "test/test.txt"}])
```

####Usage

```elixir
:dets.insert(table, {:k, 1}) #can also use :name to access table as that is what table is
:dets.lookup(:file_table, :a) # => [a: 3]
:dets.close(:file_table) #If you don't do this, the table will be repaired the next time it is opened.
```

