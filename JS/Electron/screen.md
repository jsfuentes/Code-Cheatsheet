# Screen

Add window to external display

```javascript
const { app, BrowserWindow, screen } = require('electron')

let win

app.on('ready', () => {
  let displays = screen.getAllDisplays()
  let externalDisplay = displays.find((display) => {
    return display.bounds.x !== 0 || display.bounds.y !== 0
  })

  if (externalDisplay) {
    win = new BrowserWindow({
      x: externalDisplay.bounds.x + 50,
      y: externalDisplay.bounds.y + 50
    })
    win.loadURL('https://github.com')
  }
})
```

# [Display Object](https://www.electronjs.org/docs/api/structures/display#display-object)

- `id` Number - Unique identifier associated with the display.
- `bounds` [Rectangle](https://www.electronjs.org/docs/api/structures/rectangle) //x from left and y from top
- `size` [Size](https://www.electronjs.org/docs/api/structures/size)
- `workArea` [Rectangle](https://www.electronjs.org/docs/api/structures/rectangle)
- `workAreaSize` [Size](https://www.electronjs.org/docs/api/structures/size)
- `internal` Boolean - `true` for an internal display and `false` for an external display