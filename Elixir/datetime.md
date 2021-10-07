# [DateTime](https://hexdocs.pm/elixir/DateTime.html)

Many functions in this module require a time zone database. By default, it uses the default time zone database returned by [`Calendar.get_time_zone_database/0`](https://hexdocs.pm/elixir/Calendar.html#get_time_zone_database/0), which defaults to [`Calendar.UTCOnlyTimeZoneDatabase`](https://hexdocs.pm/elixir/Calendar.UTCOnlyTimeZoneDatabase.html) which **only handles "Etc/UTC"** datetimes and returns `{:error, :utc_only_time_zone_database}` for any other time zone.

- need lib to handle timezones, **use timex package**

```elixir
dt = DateTime.utc_now()
dt = ~U[2020-05-29 02:15:00Z] #Only UTC Timezone

# Change to first of month
%{dt | day: 1, hour: 0, minute: 0, second: 0, microsecond: {0, 0}}

dt |> DateTime.add(60, :second) #Expected :second, :millisecond, :microsecond, :nanosecond
```

### Native DateTime

**No timezone data** so because of daylight savings could occur twice or never

```elixir
naive = ~N[2000-01-01 23:00:07]
naive.year #2000
naive.second #7
dt.year #2020

NaiveDateTime.add(~N[2014-10-02 00:29:10.021], 21, :second) 
```

### UNIX

```elixir
nowUTC = DateTime.utc_now() |> DateTime.to_unix(:millisecond)

DateTime.from_unix(1594370959) #{:ok, ~U[2020-07-10 08:49:19Z]}
DateTime.from_unix!(1594370959)
```

#### Comparison

Normally < and > don't work well

```elixir
DateTime.compare(now, se.start_time) #:lt, :eq, :gt
DateTime.compare(~U[2021-08-21 04:00:00Z], ~U[2021-09-21 04:00:00Z]) #:lt
```

```elixir
case DateTime.compare(end_datetime, now) do
	:lt ->
    get_current_month_period(now, Timex.shift(start_datetime, months: 1))

	:eq ->
		%{period_start: start_datetime, period_end: end_datetime}

	:gt ->
		%{period_start: start_datetime, period_end: end_datetime}
end
```

