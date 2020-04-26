# Segment

A single library to include that then loads other analytics tools

Can also add integration sources with no code to sync to downstream data warehouses

## Server vs Client Tracking

All libs just wrap the HTTP API

Client:

- Needed for some tools
- Richer User Data(cookies, IP, user agent, referrer, UTMs, mobile device info)
- Automatically assigns userId and stores in local storage

Server:

- More accurate as can't be blocked by adblockers/etc

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
analytics.track("Demo Recorded");
```

Don't bother calling identify for anonymous client users, let Segment do its random id thing stored in local storage

### Server Usage

No automatic userID, needs to be set

#### Node Init

```js
const Analytics = require("analytics-node");
const analytics = new Analytics(conf.get("SEGMENT_KEY"));

analytics.track({userId: id, event: "Demo Recorded"})
analytics.identify({userId: id, traits: {email, username}})
```

