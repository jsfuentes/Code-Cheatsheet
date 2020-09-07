# Redix

## Setup

```elixir
       {:castore, ">= 0.0.0"}, # adds ssl support
       {:redix, ">= 0.0.0"},
```

[Ssl](https://hexdocs.pm/redix/Redix.html#module-ssl)

Redix uses bidirecitonal TCP so can handle multiple request at same time. Might new  [Redix pool](https://hexdocs.pm/redix/real-world-usage.html) if maps 1to1 to user requests

```elixir
children = [
  {Redix, name: :redix}
]
```

Then user with name `Redix.command(:redix, ["PING"])`

## Usage

Redix is simple: it doesn't wrap Redis commands with Elixir functions. It only provides functions to send any Redis command to the Redis server. A Redis *command* is expressed as a list of strings making up the command and its arguments.

Connections are started via `start_link/0,1,2`:

```elixir
{:ok, conn} = Redix.start_link(host: "example.com", port: 5000)
{:ok, conn} = Redix.start_link("redis://localhost:6379/3", name: :redix)
```

Commands can be sent using `Redix.command/2,3`:

```elixir
Redix.command(conn, ["SET", "mykey", "foo"])
#=> {:ok, "OK"}
Redix.command(conn, ["GET", "mykey"])
#=> {:ok, "foo"}
```

Pipelines are just lists of commands sent all at once to Redis for which Redis replies with a list of responses. They can be used in Redix via `Redix.pipeline/2,3`:

```
Redix.pipeline(conn, [["INCR", "foo"], ["INCR", "foo"], ["INCRBY", "foo", "2"]])
#=> {:ok, [1, 2, 4]}
```

`Redix.command/2,3` and `Redix.pipeline/2,3` always return `{:ok, result}` or `{:error, reason}`. If you want to access the result directly and raise in case there's an error, bang! variants are provided:

```
Redix.command!(conn, ["PING"])
#=> "PONG"

Redix.pipeline!(conn, [["SET", "mykey", "foo"], ["GET", "mykey"]])
#=> ["OK", "foo"]
```