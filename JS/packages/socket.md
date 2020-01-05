# Socket.io

Easy abstraction for sockets with lib for client and NodeJS server

```bash
npm install socket.io
npm install socket.io-client
```

- Supports JSON, ArrayBuffer, and Blob

- Highly **robust**: Autoreconnects; starts with longpolling before upgrading to Websockets if supported

## General Usage

### IO

**Emit** sends event to all connect clients

```javascript
//server
io.emit('some event', { someProperty: 'some value', otherProperty: 'other value' });
//client
socket.on('some event', (data) => { 
	//....
});
```

Rooms allow you to create seperate channels

### Socket 

- `.id` - each socket by default joins a room identified by this random id

Emit event to specific socket

```js
//send to socket.id
socket.emit('request', ...); 
//send to id
socket.broadcast.to(id).emit('my message', msg);
```

Only server-side, broadcast sends message to everyone except socket that starts it

```js
socket.broadcast.emit('request', {...});
```

## Namespace

Setup custom namespace's server-side

```js
const nsp = io.of('/my-namespace');
nsp.on('connection', function(socket){
  console.log('someone connected');
});
nsp.emit('hi', 'everyone!');
```

Then connect to it client side 

```js
const socket = io('/my-namespace');
```

### Room

Within each namespace, you can have many rooms that can be joined or left

```js
io.on('connection', function(socket){
  socket.join('some room');
});

//And then simply use to or in (they are the same) when broadcasting or emitting:
io.to('some room').emit('some event');
```

To leave a channel you call leave in the same fashion as join. Both methods are asynchronous and accept a callback argument.

## Server/Client Usage

### Server

Setuping up with express generator's bin/www is a little tricky

Socket.js

```js
//Sockets
const socket_io = require("socket.io");
const debug = require("debug")("app:socket");

const io = socket_io();
const socketAPI = {};
socketAPI.io = io;
io.on("connection", socket => {
  debug("connected");
});

io.on("disconnect", evt => {
  debug("some people left");
});

socketAPI.sendMessage = () => {
  io.emit("message", { banana: 1 });
};

module.exports = socketAPI;
```

*Require this file to access the right fts in the routes*

bin/www

```javascript
let server = http.createServer(app);

const io = socketApi.io;
io.attach(server);
```

### Client

```javascript
import io from 'socket.io-client';

//by default connects to server that served it, 1st arg is the route to connect on
const socket = io(); 
socket.on("message", evt => {
  console.log("Recieved Msg", evt);
  socket.emit("message", evt);
});
```

## PM

**Client-side (sending message)**

```js
socket.emit("private", { msg: chatMsg.val(), to: selected.text() });
```

where `to` refers to the id to send a private message to and `msg` is the content.

**Client-side (receiving message)**

```js
socket.on("private", function(data) {   
   chatLog.append('<li class="private"><em><strong>'+ data.from +' -> '+ data.to +'</strong>: '+ data.msg +'</em></li>');
});
```

where `chatLog` is a div displaying the chat messages.

**Server-side**

```js
client.on("private", function(data) {       
    io.sockets.sockets[data.to].emit("private", { from: client.id, to: data.to, msg: data.msg });
    client.emit("private", { from: client.id, to: data.to, msg: data.msg });
});
```

## Extra

Authentication can be done by appending user token to query string 

Or socketio-auth