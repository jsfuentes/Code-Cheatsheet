# Deep Links

How do you have a link open in your app?

If you are using electron-builder, edit your build key in the package.json

```json
 "build": {
    "productName": "Slingshow",
    "appId": "org.jn.Slingshow",
    "protocols": {
      "name": "slingshow-protocol",
      "schemes": [
        "slingshow"
      ]
    },
  }
```

main.js

```javascript
// This will catch clicks on links such as <a href="slingshow://abc=1">open in slingshow</a>
app.on("open-url", (event, data) => {
  event.preventDefault();
  console.log("URL OPENED", event, data);
});

app.setAsDefaultProtocolClient("slingshow");
```

Data will just be the url like `Slingshow://help=me`

