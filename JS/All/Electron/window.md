# Windows

```javascript
win.on('resize', )
win.on('move', )
win.on('close', )
win.on('focus', )
win.on('blur', )
win.on('close', )
win.webContents.on('crashed', )
win.removeListener('resize', ft)

win.loadURL(modalPath)
win.show()
win.focus()
```

## Main Process

Watch out `__dirname` changes depending on your folder(relevant for React boilerplate web pack)

```javascript
const {app, BrowserWindow} = require('electron')
const path = require('path')

let mainWindow;

app.on('ready', () => {
    mainWindow = new BrowserWindow({
      width: 800,
      height: 600,
      webPreferences: {
        preload: path.join(__dirname, 'preload.js')
      }
    })
  
    mainWindow.loadURL(`file://${__dirname}/app.html`);

  mainWindow.webContents.on("did-finish-load", () => {
    if (!mainWindow) {
      throw new Error('"mainWindow" is not defined');
    }
    mainWindow.show();
    mainWindow.focus();
  });

  mainWindow.on("closed", () => {
    mainWindow = null;
  });

})
```

## Renderer Process

Use remote module to create ne windows

```javascript
const {BrowserWindow} = require('electron').remote;

let display = screen.getPrimaryDisplay();
let screenHeight = display.bounds.height;
const win = new BrowserWindow({
  show: false,
  frame: false,
  width: width,
  height: height,
  x: 0, //left offset
  y: screenHeight - height, //top offset
  hasShadow: false,
  transparent: true,
  alwaysOnTop: true,
  resizable: false,
  movable: false,
  webPreferences: { devTools: true, nodeIntegration: true }
});
win.loadURL(
  `file://${__dirname}/app.html?id=record&${queryString.stringify(options)}`
);
win.focus();
win.show();
win.webContents.openDevTools();
```

## Dialog Box

```javascript
const options = {
  type: 'info', 
  title: 'Render Process Hanging',
  message: 'This process is hanging.',
  buttons: ['Reload', 'Close']
};

dialog.showMessageBox(options, (index) => {
  if(index === 0) win.reload();
  else win.close();
})
```

