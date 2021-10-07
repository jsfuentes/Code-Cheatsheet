# Structs

Structs are extensions built on top of maps that provide default values and compile-time guarantees that only the defined fields exist.

Structs are **bare** maps which means you can't enumerate or [] a struct. But you can use `Map.` functions

### Creating

```elixir
defmodule User do
	defstruct name: "John", age: 27
end
```

```elixir
iex> %User{}
%User{age: 27, name: "John"}
iex> %User{name: "Jane"}
%User{age: 27, name: "Jane"}
```

