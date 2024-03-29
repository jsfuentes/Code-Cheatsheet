# Channels

[Phoenix Channels](https://hexdocs.pm/phoenix/channels.html) are basically sockets. Senders broadcast messages about topics. Receivers subscribe to topics so that they can get those messages.

See Presence to extend functionality

```bash
mix phx.gen.channel [module_name] #user
```

### Server

Already setup by default in endpoint.ex and user_socket.ex, most of the work is client side

##### To add current user to socket

lib/ss_web/channels/user_socket.ex

```elixir
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
    #{:ok, :payload, socket} #paylaod can be object
  end
  
  def join("subevent:*", payload, socket) do
    assignedSocket = assign(socket, :event_id, event_id)
    #broadcast can only be called after socket finishes joining
    send(self, :after_join)
    {:ok, assignedSocket}
  end
  
   def handle_info(:after_join, socket) do
      push(socket, "feed", %{list: feed_items(socket)})
      {:noreply, socket}
    end
  
  #eChannel.push("new_msg", {body: "hi"});
  def handle_in("new_msg", %{"body" => body}, socket) do
  user_id = socket.assigns.user_id
    broadcast!(socket, "new_msg", %{body: body})
    # Must use Endpoint to broadcast to external channel
    ReactPhoenixWeb.Endpoint.broadcast("user:#{user_id}", "new_msg", %{body: body})
    {:reply, :ok, socket}
    {:reply, {:error, %{errors: changeset}}, socket)
    #best practice to respond with error or ok so client can properly deal 
  end
  
  #when you broadcast user_joined this intercepts
  intercept ["user_joined"]

  def handle_out("user_joined", msg, socket) do
    if Accounts.ignoring_user?(socket.assigns[:user], msg.user_id) do
      {:noreply, socket}
    else
      push(socket, "user_joined", msg)
      {:noreply, socket}
    end
  end
  
  def terminate(reason, socket) do
  	#can't do send self here
    broadcast socket, "user_left", payload
    #will not send to socket
    broadcast_from socket, "user_left", payload
    {:noreply, socket}
  end
end
```

`broadcast` will notify all clients on socket's topic and invoke their handle_out callback if defined for filtering/customization

### [Client](https://hexdocs.pm/phoenix/js/#channelleave)

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

channel.push(event, payload)
  .receive('ok', data => debug(data))
  .receive('error', reasons => debug("er", reasons))
  .receive('timeout', () => debug("timeout"))

function onClick() {
  channel.push("new_msg", {body: "test"})
}
```

### Other Client

```js
socket.onError( () => )
socket.onClose( () => )
channel.onError( () => console.log("error!") )
channel.onClose( () => console.log("gone gracefully") )
// Unsubscribe the do_stuff handler
const ref1 = channel.on("event", do_stuff)
channel.off("event", ref1)

// Unsubscribe all handlers from event
channel.off("event")
channel.leave().receive("ok", () => alert("left!") )
```

