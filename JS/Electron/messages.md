# Messages

## From Main to Render

Main

```js
win.webContents.send('async-msg', 'pinggg');
```

Renderer

```js
ipc.on('reply', (event, arg) => {
  console.log("Message is ", arg);
})
```

### From Render to Main

main.js

```js
import { ipcMain } from "electron";

ipcMain.on("async-msg", (event, arg) => {
  console.log(arg);
  event.sender.send('reply', 'pong');
});
```

renderer.js

```js
const ipc = require("electron").ipcRenderer;

ipc.send("start-recording", "ping");

ipc.on('reply', (event, arg) => {
  console.log("Message is ", arg);
})
```

