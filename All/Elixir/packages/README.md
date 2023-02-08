# Packages

To add a package, you need to add a line to 

mix.exs

```elixir
  defp deps do
    [
			#.....
      {:plug_cowboy, "~> 2.0"},
      {:httpoison, "~> 1.6"}
    ]
  end
```

Then run `mix deps.get`

### Version

```elixir
# Only version 2.0.0
"== 2.0.0"

# Anything later than 2.0.0
"> 2.0.0"

# 2.0.0 and later until 2.1.0
">= 2.0.0 and < 2.1.0"
# Equivalent to
"~> 2.0.0"
```

### [Updating](https://inquisitivedeveloper.com/lwm-elixir-58/)

```bash
mix hex.outdated #to see what packages have newer versions
mix deps.update --all #updates minor versions of all deps 
# Need to manually change mix.exs to update major version
```

### Packages of Interest

- [guardian](https://github.com/ueberauth/guardian)
- Genstage, broadway
