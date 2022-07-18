# Electron

Use HTML, CSS, and JS to build desktop apps on Windows, Max, and Linux

The react-boilerplate required a lot of deletion, also look into the next.js boilerplate

## Basics

Every app starts with main script that controls app lifecycle, can pretend its like Node.js 

Each browser window is a seperate renderer process

Use the `ipc` (inter-process communication) module to send and recieve sync/async messages

Create invisible browser window to run tasks without impact main app performance

## Usage

`__dirname` to get load assets in main

## Simplest App

main.js

```javascript
const {app, BrowserWindow} = require('electron')
const path = require('path')

// Keep global b/c will be closed when garbage collected
let mainWindow

function createWindow () {
  mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })
  mainWindow.loadFile('index.html')
  // mainWindow.webContents.openDevTools()
  mainWindow.on('closed', function () {
    // Usually store windows in array and delete those
    mainWindow = null
  })
}

// Ready to createWindows and use other APIS
app.on('ready', createWindow)

// Quit when all windows are closed.
app.on('window-all-closed', function () {
  // On macOS, common to keep open
  if (process.platform !== 'darwin') app.quit()
})

app.on('activate', function () {
  // On macOS, common to recreate app
  if (mainWindow === null) createWindow()
})
```

preload.js

```javascript
// Node.js APIs available in preload process, same sandbox as Chrome extension
window.addEventListener('DOMContentLoaded', () => {
  //....
})
//....
```

## Local File

### [`app.getPath(name)`](https://electronjs.org/docs/api/app#appgetpathname)

- `name` String - You can request the following paths by the name:
  - `home` User's home directory.
  - `appData` Per-user application data directory, which by default points to:
    - `%APPDATA%` on Windows
    - `$XDG_CONFIG_HOME` or `~/.config` on Linux
    - `~/Library/Application Support` on macOS
  - `userData` The directory for storing your app's configuration files, which by default it is the `appData` directory appended with your app's name.
  - `cache`
  - `temp` Temporary directory.
  - `exe` The current executable file.
  - `module` The `libchromiumcontent` library.
  - `desktop` The current user's Desktop directory.
  - `documents` Directory for a user's "My Documents".
  - `downloads` Directory for a user's downloads.
  - `music` Directory for a user's music.
  - `pictures` Directory for a user's pictures.
  - `videos` Directory for a user's videos.
  - `logs` Directory for your app's log folder.
  - `pepperFlashSystemPlugin` Full path to the system version of the Pepper Flash plugin.