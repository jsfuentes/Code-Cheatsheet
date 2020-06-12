# Segment

A single library to include that then loads other analytics tools

Can also add integration sources with no code to sync to downstream data warehouses

Best naming convention is **OBJECT ACTION** like "Event Created" and only track the flows you want not everything

## Server vs Client Tracking

All libs just wrap the HTTP API

Client:

- Needed for some tools(no server-side full-story)
- Richer User Data(cookies, IP, user agent, referrer, UTMs, mobile device info)
- Automatically assigns userId and stores in local storage

Server:

- More accurate as can't be blocked by adblockers/etc
- No automatic userID, must be explicitly set


### Client Usage

Every event automatically grabs page info and user agent

```js
/* global analytics */ //eslint fix
analytics.identify([userId], [traits], [options], [callback]);

analytics.identify(id, {
  email: email,
  status: source,
});

analytics.track(event, [properties], [options], [callback]);
analytics.track("Demo Recorded", {video_id});
```

Don't bother calling identify for anonymous client users, let Segment do its random id thing stored in local storage

### Server Usage

#### Elixir/Phoenix

[Unoffical support](https://github.com/stueccles/analytics-elixir)

mix.ex

```elixir
{:segment, "~> 0.2.3"}
```

config.exs

```elixir
config :segment,
  write_key: "2iFFnRsCfi" #Segment API KEY
```

application.ex in the supervisor list

```elixir
{Segment, Application.get_env(:segment, :write_key)}
```

##### Usage

```elixir
Segment.Analytics.track(user_id, event, %{property1: "", property2: ""})
Segment.Analytics.identify(user_id, %{trait1: "", trait2: ""})
```

#### Node Init

```js
const Analytics = require("analytics-node");
const analytics = new Analytics(conf.get("SEGMENT_KEY"));

analytics.track({userId: id, event: "Demo Recorded"})
analytics.identify({userId: id, traits: {email, username}})
```

#### 