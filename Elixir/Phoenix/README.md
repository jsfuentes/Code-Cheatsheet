# Phoenix

Web servers, API backends, and distributed messaging systems

Phoenix is not app, but ergonomic way to build web based interfaces

- MVC framework, Ruby on Rails like
- Real-time messaging channels allowing pub/sub out of the box
- Easy to test with high productivity & performance
- Auto hot reloading, Postgres default

## Phoenix Layers

- [Endpoint](https://hexdocs.pm/phoenix/endpoint.html)
  - the start and end of the request lifecycle
  - handles all aspects of requests up until the point where the router takes over
  - provides a core set of plugs to apply to all requests
  - dispatches requests into a designated router
- [Router](https://hexdocs.pm/phoenix/routing.html)
  - parses incoming requests and dispatches them to the correct controller/action, passing parameters as needed
  - provides helpers to generate route paths or urls to resources
  - defines named pipelines through which we may pass our requests
  - Pipelines - allow easy application of groups of plugs to a set of routes
- [Controllers](https://hexdocs.pm/phoenix/controllers.html)
  - provide functions, called *actions*, to handle requests
  - actions:
    - prepare data and pass it into views
    - invoke rendering via views
    - perform redirects
- [Views](https://hexdocs.pm/phoenix/views.html)
  - render templates
  - act as a presentation layer
  - define helper functions, available in templates, to decorate data for presentation
- [Templates](https://hexdocs.pm/phoenix/templates.html)
  - files containing the contents that will be served in a response
  - provide the basic structure for a response, and allow dynamic data to be substituted in
  - are precompiled and fast
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



