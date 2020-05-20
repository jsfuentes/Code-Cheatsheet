# Phoenix

Web servers, API backends, and distributed messaging systems

Phoenix is ergonomic way to build web interfaces

- MVC framework, Ruby on Rails like
- Real-time messaging [Channels](https://hexdocs.pm/phoenix/channels.html) allowing pubsub and websockets out of the box
- Easy to test with high productivity & performance(**observer tool** can be used in prod, to find bottlenecks just see which process has a big message queue)
- Auto hot reloading, Postgres default
- **Presence** lets you replicate data across clients easily like which users are online

## Phoenix Layers

- [Endpoint](https://hexdocs.pm/phoenix/endpoint.html) - *lib/hello_web/endpoint.ex*
  - the start and end of the request lifecycle
  - uses Plugs to do stuff like serve static files, log info, parse bodys => then routes to router
- [Router](https://hexdocs.pm/phoenix/routing.html) *- lib/hello_web/router.ex*
  - parses incoming requests and dispatches them to the correct controller/action, passing parameters as needed
  - Pipelines - groups plugs that requests can go through
- [Controllers](https://hexdocs.pm/phoenix/controllers.html) - *lib/hello_web/controllers/page_controller.ex*
  - provide functions, called *actions*, to handle requests
  - actions:
    - prepare data then render views
    - perform redirects
- [Views](https://hexdocs.pm/phoenix/views.html) - *lib/hello_web/views/page_view.ex*
  - controllers render templates, and views called implicitly
  - define helper functions, available in templates, to decorate data for presentation
- [Templates](https://hexdocs.pm/phoenix/templates.html) - *lib/hello_web/templates/page/index.html.eex*.
  - files that will be served allowing dynamic data/code
  - nested in the app template found in app.html.eex
- [Channels](https://hexdocs.pm/phoenix/channels.html)
  - manage sockets for easy realtime communication
  - are analogous to controllers except that they allow bi-directional communication with persistent connections
- PubSub
  - underlies the channel layer and allows clients to subscribe to *topics*
  - abstracts the underlying pubsub adapter for third-party pubsub integration

## Other parts

### Plug

simple abstraction for dealing with different web servers

- Spec to create composable functions to build pipeline for requests to response
- Plug.Conn struct gives function for working with connections, session, body etc(both req and res object)
- Function Plugs -> recieves a connection and options and return connection
- Module plug is a module that must export init and call, extension of function

### Cowboy

most popular small, fast, modular HTTP server written in Erlang that underlies Phoenix

### Ecto

A DSL for writing queries and interacting with databases

### Contexts

Dedicated Modules that expose and group related functionality

