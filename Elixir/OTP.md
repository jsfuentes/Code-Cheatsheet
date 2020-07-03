# OTP

 (Open Telecom Platform) is a collection of framework/lib/tools written in Erlang

# [Erlang Term Storage (ETS)](https://elixirschool.com/en/lessons/specifics/ets/)

ETS is a robust in-memory store for Elixir and Erlang objects that comes included. ETS is capable of storing large amounts of data and offers constant time data access.

Tables in ETS are created and owned by individual processes. When an owner process terminates, its tables are destroyed. You can have as many ETS table as you want, the only limit is the server memory. A limit can be specified using the `ERL_MAX_ETS_TABLES` environment variable.

Owned by process that creates it, doen't have bottleneck of agent.

```elixir
table_reference = :ets.new(:table_name, [:set])
:ets.insert
```

### Uses

- persisent shared state(tzdata, )
- ephemeral shared state(cache)
- IPC

