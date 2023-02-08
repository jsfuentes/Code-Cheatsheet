# File

- Mostly named after UNIX equivalents like rm/1, mkdir/1, mkdir_p/1, cp_r/2, rm_rf/1
- Two variants, one regular and one with trailing bang. Use bang if you don't handle error

Get raw contents

```elixir
case File.read(file) do
  {:ok, body}      -> # do something with the `body`
  {:error, reason} -> # handle the error caused by `reason`
end
File.read!("existing") # "... contents ..."
File.read!("unknown") #**(File.Error) ...
```

Open for read and write

```elixir
{:ok, file} = File.open("hello", [:write]) # {:ok, #PID<0.47.0>}
IO.binwrite(file, "world") #:ok
File.close(file) #:ok
File.read("hello") #{:ok, "world"}
```

## Path

```elixir
iex> Path.join("foo", "bar")
"foo/bar"
iex> Path.expand("~/hello")
"/Users/jose/hello"
```

