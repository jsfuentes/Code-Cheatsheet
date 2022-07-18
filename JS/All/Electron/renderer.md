# Renderer Process

Access remote

```js
const { dialog } = require('electron').remote
console.log(dialog);
```

Make file that works in both

```js
const electron = require("electron");
const dialog = electron.dialog || electron.remote.dialog; //ensure works in both main and renderer
```

