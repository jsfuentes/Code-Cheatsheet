# Electron-is-Dev

Simplest package ever, but it is recommended by the electron website so it must add value

```npm  install electron-is-dev```

```js
const isDev = require('electron-is-dev');

if (isDev) {
	console.log('Running in development');
} else {
	console.log('Running in production');
}
```

## The actual code lol

```js
'use strict';
const electron = require('electron');

const app = electron.app || electron.remote.app;

const isEnvSet = 'ELECTRON_IS_DEV' in process.env;
const getFromEnv = parseInt(process.env.ELECTRON_IS_DEV, 10) === 1;

module.exports = isEnvSet ? getFromEnv : !app.isPackaged;
```

