# Channels

[Phoenix Channels](https://hexdocs.pm/phoenix/channels.html) are basically sockets. Senders broadcast messages about topics. Receivers subscribe to topics so that they can get those messages.

See Presence to extend functionality

### Server

Already setup by default, work is client side

Lib/ss_wb/endpoint.ex

```elixir
  socket "/socket", SsWeb.UserSocket,
    websocket: true,
    longpoll: false
```

lib/ss_web/channels/user_socket.ex

```elixir
defmodule PhoenixPair.UserSocket do
  use Phoenix.Socket

  channel "challenges:*", PhoenixPair.ChallengeChannel
  
  def connect(_params, socket, _connect_info) do
    IO.puts "CONNTECTING BABY"
    #......
  end
end

defmodule SsWeb.UserSocket do
  use Phoenix.Socket

  ## Channels
  channel "room:*", SsWeb.RoomChannel
  
  def connect(_params, socket, _connect_info) do
    IO.puts "CONNTECTING BABY"
    {:ok, assign(socket, :current_user, user)} #assign lets you store state(key-value) to this socket
  end
end
```

Whenever a client sends a message whose topic starts with "room:", it will be routed to our `RoomChannel`.

### Channels

Like controllers, but have incoming and outgoing events and connections persist

Have `join/3`, `terminate/2`, `handle_in/3`, and `handle_out/3`

lib/ss_web/channels/room_channel.ex

```elixir
defmodule SsWeb.RoomChannel do
  use Phoenix.Channel

  def join("room:lobby", _message, socket) do
    {:ok, socket}
    {:ok, :payload, socket} #paylaod can be object
  end
  
  def join("room:" <> _private_room_id, _params, _socket) do
    {:error, %{reason: "unauthorized"}}
  end
  
    def handle_in("new_msg", %{"body" => body}, socket) do
    broadcast!(socket, "new_msg", %{body: body})
    {:noreply, socket}
  end
  
  def handle_out("user_joined", msg, socket) do
  if Accounts.ignoring_user?(socket.assigns[:user], msg.user_id) do
    {:noreply, socket}
  else
    push(socket, "user_joined", msg)
    {:noreply, socket}
  end
end
end
```

`broadcast` will notify all clients on socket's topic and invoke their handle_out callback if defined for filtering/customization

### Client

When a client successfully establishes this connection, Phoenix Channels initializes an instance of `%Phoenix.Socket{}`. The channel server then retains awareness of this `socket` instance and maintains state within that instance via calls to `socket.assign`

```js
import { Socket } from 'phoenix';
const socket = new Socket("/socket", {params: {token: <your auth token>}})
socket.connect({body: "params passed to connect"});

const channel = socket.channel(`challenges:${challengeId}`);
channel.join()
  .receive("ok", resp => { console.log("Joined successfully", resp) })
  .receive("error", resp => { console.log("Unable to join", resp) })

channel.on("new_msg", payload => {
  //payload is exactly as passed, no wrapper
})

function onClick() {
  channel.push("new_msg", {body: "test"})
}
```



