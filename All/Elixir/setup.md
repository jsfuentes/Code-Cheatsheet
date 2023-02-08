# Setup

#### Simplest

```bash
brew install elixir
```

When you install Elixir, you will have three new executables: `iex`, `elixir` and `elixirc`

### Asdf

### Basic Usage

##### Simplest

simple.exs

```elixir
IO.puts "Hello world"
```

elixir simple.exs

##### Boilerplate

```bash
mix new example --sup
cd example
mix compile
```

#### Usage

```bash
 iex -S mix
 iex> recompile()
 iex > IEx.configure(inspect: [limit: :infinity])
```

Can use the interactive prompt to test all the modules

##### Tricks

```elixir
iex(1) > 4
# 4, v accessing previous line
iex(2) > v() + 4
# 8
```

*Must restart server when you move/rename files or err*

#### Format

```bash
mix format
```

## Hex package Manager

To install hex if not installed

```
mix local.hex
```

### Dependencies

mix.exs configures the project and had dips

- project has project config like name & version
- application is used to generate app file
- private deps is invoked from project and has reps

