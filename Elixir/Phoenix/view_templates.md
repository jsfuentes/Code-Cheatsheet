# Views

Render templates and are presentation layer processing raw data for use

Must match name of controller for auto usage

lib/react_phoenix_web/views/event_view.ex

```elixir
defmodule ReactPhoenixWeb.EventView do
  use ReactPhoenixWeb, :view
  alias ReactPhoenixWeb.EventView

  def render("index.json", %{events: events}) do
    %{data: render_many(events, EventView, "event.json")}
  end

  def render("show.json", %{event: event}) do
    %{data: render_one(event, EventView, "event.json")}
  end

  def render("event.json", %{event: event}) do
    sortedSubEvents =
      if Ecto.assoc_loaded?(event.subevents),
        do: Enum.sort_by(event.subevents, & &1.start_time),
        else: []
        
    %{
      id: event.id,
      title: event.title,
      description: event.description,
      start_time: event.start_time,
      host_name: event.host_name,
      host_description: event.host_description,
#event has_many :subevents, ReactPhoenix.Events.Subevent
      subevents: render_many(sortedSubEvents, EventView, "subevent.json", as: :subevent)
    }
  end

  def render("subevent.json", %{subevent: subevent}) do
    %{
      id: subevent.id,
      title: subevent.title,
      description: subevent.description,
      link: subevent.link,
      type: subevent.type
    }
  end
end
```

#### Usage

```elixir
render(conn, "show.json", event: event)

public_subevent = Phoenix.View.render_one(subevent, ReactPhoenixWeb.EventView, "subevent.json")

Chat.list_chat_messages(socket.assigns.user_id, cc.id, last_time_seen)
|>Phoenix.View.render_many(ReactPhoenixWeb.ChatMessageView, "preloaded_message.json")
```

## Templates

Phoenix template engine is [`EEx`](https://hexdocs.pm/eex/EEx.html)(Embedded Elixir)

Like ruby `<% %>` to just run code and `<%= %>` to insert into HTML

lib/hello_web/templates/hello/index.html.eex

```html
<div class="phx-hero">
  <h2>Hello World, from <%= @messenger %>!</h2>
</div>
```

`messenger` was passed in with `render(conn, "index.html", messenger: "j")`

Notice inserted in an app layout found at

lib/hello_web/templates/layout/app.html.eex

```html
<%= render @view_module, @view_template, assigns %>
```

### Nesting Templates

lib/hello_web/templates/user/user.html.eex

```html
<strong> <%= first_name(@user) %> </strong>
```

Another template

```html
<h1> Showing Users </h1> <%= render "user.html", user: @user %>
```

