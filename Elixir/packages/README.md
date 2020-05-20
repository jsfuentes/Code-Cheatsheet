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

### Packages of Interest

- [guardian](https://github.com/ueberauth/guardian)

