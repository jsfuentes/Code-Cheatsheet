# DateTime

Many functions in this module require a time zone database. By default, it uses the default time zone database returned by [`Calendar.get_time_zone_database/0`](https://hexdocs.pm/elixir/Calendar.html#get_time_zone_database/0), which defaults to [`Calendar.UTCOnlyTimeZoneDatabase`](https://hexdocs.pm/elixir/Calendar.UTCOnlyTimeZoneDatabase.html) which only handles "Etc/UTC" datetimes and returns `{:error, :utc_only_time_zone_database}` for any other time zone.

```elixir
dt = ~U[2020-05-29 02:15:00Z]

dt |> DateTime.add(60, :second)
```

