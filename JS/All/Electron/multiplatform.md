# Differences Between Platforms

## Mac

Icon in taskbar is application icon(.ico or .icns)

## Linux

Icon is taskbar is window icon

```js
mainWindow = new BrowserWindow({ 
  title: 'ElectronApp', 
  icon: __dirname + '/app/assets/img/icon.png', 
});
```