# Time

See timex for more advanced stuff

#### DateTime

Utc_now is the same type as timestamps from db

```elixir 
now = DateTime.utc_now() #~U[2020-12-07 01:09:48.868084Z]
nowUTC = DateTime.utc_now() |> DateTime.to_unix() #1607303503
```

Compare

```elixir
def is_current_subevent(se) do
  now = DateTime.utc_now()
  start_cmp = DateTime.compare(now, se.start_time)
  end_cmp = DateTime.compare(now, se.end_time)
  start_cmp === :gt && end_cmp === :lt
end
```

#### Naive DateTime

```elixir 
now = NaiveDateTime.utc_now()
# 7 hour diff PST, so 19
tomorrow_noon =
  NaiveDateTime.new(now.year, now.month, now.day, 19, 0, 0)
  |> (fn {:ok, d} -> d end).()
  |> NaiveDateTime.add(60 * 60 * 24, :second)

tomorrow_one = tomorrow_noon |> NaiveDateTime.add(60 * 60, :second)
```

#### Erlang Standard

Get current time with `:calendar.universal_time()` or `:calendar.local_time()`

