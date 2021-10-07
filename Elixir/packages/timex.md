#  [Timex](https://hexdocs.pm/timex/getting-started.html)

```elixir
[{:timex, "~> 3.5"}]
```

## Usage

```elixir
> use Timex
> Timex.today
~D[2016-02-29]

> datetime = Timex.now
#<DateTime(2016-02-29T12:30:30.120+00:00Z Etc/UTC)

> Timex.now("America/Chicago")
#<DateTime(2016-02-29T06:30:30.120-06:00 America/Chicago)

> Duration.now
#<Duration(P46Y6M24DT21H57M33.977711S)>

> {:ok, default_str} = Timex.format(datetime, "{ISO:Extended}")
{:ok, "2016-02-29T12:30:30.120+00:00"}

> {:ok, relative_str} = Timex.shift(datetime, minutes: -3) |> Timex.format("{relative}", :relative)
{:ok, "3 minutes ago"}

> strftime_str = Timex.format!(datetime, "%FT%T%:z", :strftime)
"2016-02-29T12:30:30+00:00"

> Timex.parse(strftime_str, "{ISO:Extended}")
{:ok, #<DateTime(2016-02-29T12:30:30.120+00:00 Etc/Utc)}

> Timex.parse!(strftime_str, "%FT%T%:z", :strftime)
#<DateTime(2016-02-29T12:30:30.120+00:00 Etc/Utc)

> Duration.diff(Duration.now, Duration.zero, :days)
16850

> Timex.shift(date, days: 3)
~D[2016-03-03]

> Timex.shift(datetime, hours: 2, minutes: 13)
#<DateTime(2016-02-29T14:43:30.120Z Etc/UTC)>

> timezone = Timezone.get("America/Chicago", Timex.now)
#<TimezoneInfo(America/Chicago - CDT (-06:00:00))>

> Timezone.convert(datetime, timezone)
#<DateTime(2016-02-29T06:30:30.120-06:00 America/Chicago)>

> Timex.before?(Timex.today, Timex.shift(Timex.today, days: 1))
true

> Timex.before?(Timex.shift(Timex.today, days: 1), Timex.today)
false

> interval = Timex.Interval.new(from: ~D[2016-03-03], until: [days: 3])
%Timex.Interval{from: ~N[2016-03-03 00:00:00], left_open: false,
 right_open: true, step: [days: 1], until: ~N[2016-03-06 00:00:00]}

> ~D[2016-03-04] in interval
true

> ~N[2016-03-04 00:00:00] in interval
true

> ~N[2016-03-02 00:00:00] in interval
false

> Timex.Interval.overlaps?(Timex.Interval.new(from: ~D[2016-03-04], until: [days: 1]), interval)
true

> Timex.Interval.overlaps?(Timex.Interval.new(from: ~D[2016-03-07], until: [days: 1]), interval)
false
```

## Formatting Datime

```elixir
Timex.format!(~U[2020-06-30 19:00:00Z], "{YYYY}-{0M}-{D}")

~U[2020-06-30 19:00:00Z] |>
Timex.to_datetime("America/Los_Angeles") |> Timex.format!("{WDshort} {Mshort} {D}, {kitchen} {Zabbr}") # "Tue Jun 30, 12:00PM PDT"
```



