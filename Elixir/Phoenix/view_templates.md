# Views

Render templates and are presentation layer processing raw data for use

Must match name of controller

lib/hello_web/views/hello_view.ex

```elixir
defmodule HelloWeb.HelloView do
  use HelloWeb, :view
end
```

## Templates

standard templating engine Phoenix uses is [`EEx`](https://hexdocs.pm/eex/EEx.html), which stands for Embedded Elixir.

lib/hello_web/templates/hello/index.html.eex

```html
<div class="phx-hero">
  <h2>Hello World, from <%= @messenger %>!</h2>
</div>
```

Notice inserted in an app layout found at

lib/hello_web/templates/layout/app.html.eex

```html
<%= render @view_module, @view_template, assigns %>
```

