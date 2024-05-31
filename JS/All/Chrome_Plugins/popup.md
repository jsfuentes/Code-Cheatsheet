# Popup

In manifest

```json
  "browser_action": {
    "default_popup": "popup.html"
  },
```

In popup.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Slingshow</title>
    <script src="./build/popup.js" defer></script>
    <link rel="stylesheet" href="./tailwind.css" />
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
```

In popup.js

```jsx
import React, { useState, useEffect } from "react";
import ReactDOM from "react-dom";
import browser from "webextension-polyfill";
const debug = require("debug")("app:popup");

debug("Running popup");
function Popup() {
 	return (<div> Pop pop </div>);
}

ReactDOM.render(<Popup />, document.getElementById("root"));
```

Then you need to build the popup.js using parcel/webpack which it is then built in `build/popup.js`

- popup.js is basically like a background/service_worker script

### Size

To set size, or can expand for content

```css
html,
body {
  width: 800px;
  height: 600px;
}
```

Max Height 600px

Max Width 800px