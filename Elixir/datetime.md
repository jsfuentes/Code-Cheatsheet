# DateTime

Many functions in this module require a time zone database. By default, it uses the default time zone database returned by [`Calendar.get_time_zone_database/0`](https://hexdocs.pm/elixir/Calendar.html#get_time_zone_database/0), which defaults to [`Calendar.UTCOnlyTimeZoneDatabase`](https://hexdocs.pm/elixir/Calendar.UTCOnlyTimeZoneDatabase.html) which only handles "Etc/UTC" datetimes and returns `{:error, :utc_only_time_zone_database}` for any other time zone.

```elixir
dt = ~U[2020-05-29 02:15:00Z]

dt |> DateTime.add(60, :second)
```

### Native DateTime

Not linked to timezone so because of daylight savings could occur twice or never

```elixir
naive = ~N[2000-01-01 23:00:07]
naive.year #2000
naive.second #7

NaiveDateTime.add(~N[2014-10-02 00:29:10.021], 21, :second) #Expected :second, :millisecond, :microsecond, :nanosecond
```

