# Real-Time

How do you do stuff like realtime updates, push changes from server to clients?

## Websockets

[Sockets.io](https://socket.io/)

- Create a sustained connection that both sides listen to
- Remove work of constantly doing a handshake, creating a connection, and sending headers

#### Polling

Client requests updates from server on schedule

#### Long polling / Server-Sent Events

The client asks for info and the server keeps the connection open until a response, uses the EventSource API

## Kafka

Heavy duty producer consumer relationship

All these producers publish to kafka to their own or a common stream, and all these consumers can subscribe to the data streams

