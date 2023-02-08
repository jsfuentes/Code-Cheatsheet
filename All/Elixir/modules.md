# [Modules](https://hexdocs.pm/elixir/master/Module.html)

```elixir
# Alias the module so it can be called as Bar instead of Foo.Bar
alias Foo.Bar, as: Bar
alias Foo.Bar #defaults to name after .(Bar)
# Require the module in order to use its macros
require Foo
# Import functions from Foo so they can be called without the `Foo.` prefix
import Foo
# Invokes the custom code defined in Foo as an extension point
use Foo
```

## Attributes

#### Impl

When you use a module then want to implement the functions you can use `@impl true` to indicate what you think a callback is, it will do typechecking matching it

- Will error if you do it once and not every time

```elixir
@impl true
def init(state) do
  {:ok, state}
end

@impl true
def start_link do
  GenServer.start_link(__MODULE__, 0)
end
```



