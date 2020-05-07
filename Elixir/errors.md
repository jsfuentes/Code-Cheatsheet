# Errors

Elixir has three error mechanisms: errors, throws, and exits.

Instead of all these constructs, Elixir's supervisor system is better to just fail fast and restart the app in a known state

## Errors

Errors (or *exceptions*) are used when exceptional things happen in the code.

In Elixir, we avoid using `try/rescue` because **we don’t use errors for control flow**. 

```elixir
iex> :foo + 1
** (ArithmeticError) bad argument in arithmetic expression
     :erlang.+(:foo, 1)
iex> raise "oops"
** (RuntimeError) oops
iex> raise ArgumentError, message: "invalid argument foo"
** (ArgumentError) invalid argument foo
```

Try/catch => try/rescue, in practice rarely used b/c tuple with err often used instead

```elixir
iex> try do
...>   raise "oops"
...> rescue
...>   e in RuntimeError -> e
...> end
%RuntimeError{message: "oops"}
```

#### Custom Errors

```elixir
iex> defmodule MyError do
iex>   defexception message: "default message"
iex> end
iex> raise MyError
** (MyError) default message
iex> raise MyError, message: "custom message"
** (MyError) custom message
```

## Throws

`throw` and `catch` are reserved for situations where it is not possible to retrieve a value unless by using `throw` and `catch`. 

Also uncommon

## Exits

When a process dies of "natural causes" (unhandled exceptions), it sends an exit signal

