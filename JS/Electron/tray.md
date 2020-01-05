# Tray

```javascript
const { app, Menu, Tray } = require('electron')

let tray = null
app.on('ready', () => {
  tray = new Tray('/path/to/my/icon')
  const contextMenu = Menu.buildFromTemplate([
    { label: 'Item1', type: 'radio' },
    { label: 'Item2', type: 'radio' },
    { label: 'Item3', type: 'radio', checked: true },
    { label: 'Item4', type: 'radio' }
  ])
  tray.setToolTip('This is my application.')
  tray.setContextMenu(contextMenu)
})
```

## Icons

Use **Template Images** for Mac OS so it can flip on dark/light mode

Template images consist of black and an alpha channel

To mark an image as a template image, its filename should end with the word `Template`. For example:

- `xxxTemplate.png`
- `xxxTemplate@2x.png`