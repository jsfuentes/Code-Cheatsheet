# Modules

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

