# Zendesk

## API

## Update Ticket

Outside

```js
const resp = await axios.get(`${domain}/api/v2/users/${user_id}.json`, {
  headers: { Authorization: `Bearer ${access_token}` },
});
```

Inside the client

```js
$.ajax({ url: '/api/v2/tickets/5.json', type: "PUT", contentType: 'application/json', data: JSON.stringify({"ticket": {"status": "pending"}})})
```

## App

### Setup

```bash
gem install rake
gem install zendesk_apps_tools
zat new #creates start files
```

Go to any live zendesk website and add to the url  `?zat=true`

##### Usage

Start in the folder you want and should have built react app or whatever in the asset folder

```bash
zat server
```

### Client

.html

```html
<script src="https://static.zdassets.com/zendesk_app_framework_sdk/2.0/zaf_sdk.min.js"></script>
```

.js

```javascript
const client = ZAFClient.init();
client.invoke("resize", { width: "420px", height: "300px" });
client.get("ticket.id").then((data) => {
console.log("ticket.id", data["ticket.id"]);
});
client.get("currentUser").then(function (data) {
console.log("currentUser", data["currentUser"]);
});
```

### Secure Auth

```
axios.post(https://{subdomain}.zendesk.com/oauth/authorizations/new, payload);
https://slingshow.zendesk.com/oauth/authorizations/new?client_id=slingshow&redirect_uri=localhost%3A3001%2Fconnect%2Fzendesk%2Fcallback&response_type=token&scope=tickets%3Aread%20tickets%3Awrite&state=Stitch
```

```js
const payload = {
	response_type: "token",
  redirect_uri: "http://localhost:3001/connect/zendesk/callback",
	client_id: "slingshow",
	scope: "tickets:read tickets:write",
  state: "Stitch"
};
axios.post("https://slingshow.zendesk.com/oauth/authorizations/new", payload);
```

### Using Bearer

```
const config = {
    headers: { Authorization: `Bearer ${token}` }
};
const bodyParameters = { key: "value" };
axios.post( 
  'http://localhost:8000/api/v1/get_token_payloads',
  bodyParameters, config);
```

