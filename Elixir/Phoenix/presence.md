# [Presence](https://hexdocs.pm/phoenix/Phoenix.Presence.html#c:fetch/2)

Register process info on topic and replicate it across cluster.

- Simple use case would be showing whose online
- metadata should be minimized and used to store small, ephemeral state, such as a user's "online" or "away" status. Can fetch more substantial stuff by overriding the fetch/2 ft

### Usage

Probably used in channel with access to socket

```elixir
Presence.track(socket, socket.assigns.user_id, %{
      online_at: inspect(System.system_time(:second))
    });
push(socket, "presence_state", Presence.list(socket));

Presence.update(socket, socket.assigns.user_id, %{
	online_at: inspect(System.system_time(:second))
})
Presence.update(socket, socket.assigns.user_id, fn map -> Map.put(map, :name, name) end)
Presence.update( socket, socket.assigns.user_id,
&(Map.put(&1, :name, name) |> Map.put(:online_at, now)))

Presence.get_by_key(socket, socket.assigns.user_id)
MyPresence.get_by_key("room:1", "user1")
```

## Complete Example

Need to have channel already setup

 [`mix phx.gen.presence`](https://hexdocs.pm/phoenix/Mix.Tasks.Phx.Gen.Presence.html) 

Generates, ssweb/lib/channels/presence.ex

```elixir
defmodule SsWeb.Presence do
  use Phoenix.Presence, otp_app: :ss,
                        pubsub_server: Ss.PubSub
end
```

lib/hello/application.ex

```elixir
    children = [
      ...
      HelloWeb.Presence,
    ]
```

lib/channels/user_socket.ex - add user_id to socket

```elixir
defmodule SsWeb.UserSocket do
  use Phoenix.Socket
  channel "room:*", SsWeb.RoomChannel
  
  def connect(params, socket, _connect_info) do
    {:ok, assign(socket, :user_id, params["user_id"])}
  end
end
```

lib/channels/room_channel.ex

```elixir
defmodule HelloWeb.RoomChannel do
  use Phoenix.Channel
  alias HelloWeb.Presence
  
  # intercept ["presence_diff"]

  def join("room:lobby", _message, socket) do
    send(self(), :after_join)
    {:ok, :hiii, socket}
  end
  
  def handle_info(:after_join, socket) do
    push(socket, "presence_state", Presence.list(socket))
    #Presence.track links channel's process as a presence for the socket's userID with map of metadata
    {:ok, _} = Presence.track(socket, socket.assigns.user_id, %{
      online_at: inspect(System.system_time(:second))
    })
    {:noreply, socket}
  end
  
    # To alter or stop presence updates
  # def handle_out("presence_diff", msg, socket) do
  #   {:noreply, socket}
  # end
end
```

### Client

Actually (and before 1.4?) recieved "presence_diff" and "presence_state" events

Only one onSync handler allowed

```js
import {Socket, Presence} from "phoenix"

let socket = new Socket("/socket", {
  params: {user_id: window.location.search.split("=")[1]}
})

let channel = socket.channel("room:lobby", {})
let presence = new Presence(channel)

function renderOnlineUsers(presence) {
  let response = ""

  presence.list((id, {metas: [first, ...rest]}) => {
    let count = rest.length + 1
    response += `<br>${id} (count: ${count})</br>`
  }) //metas is list of users with this id

  document.querySelector("main[role=main]").innerHTML = response
}

socket.connect()

presence.onSync(() => renderOnlineUsers(presence))

channel.join()
```

##### More Client

```js
let presence = new Presence(channel)

// detect if user has joined for the 1st time or from another tab/device
presence.onJoin((id, current, newPres) => {
  if(!current){
    console.log("user has entered for the first time", newPres)
  } else {
    console.log("user additional presence", newPres)
  }
})

// detect if user has left from all tabs/devices, or is still present
presence.onLeave((id, current, leftPres) => {
  if(current.metas.length === 0){
    console.log("user has left from all devices", leftPres)
  } else {
    console.log("user left from a device", leftPres)
  }
})
// receive presence data from server
presence.onSync(() => {
  displayUsers(presence.list())
})
```

