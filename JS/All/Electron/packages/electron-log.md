# Electron-Log

Log to file in production

By default, it writes logs to the following locations:

- **on Linux:** `~/.config/{app name}/logs/{process type}.log`
- **on macOS:** `~/Library/Logs/{app name}/{process type}.log`
- **on Windows:** `%USERPROFILE%\AppData\Roaming\{app name}\logs\{process type}.log`

```js
const log = require("electron-log");
Object.assign(console, log.functions); //replace console with file logging in the main process
```

Supports following log levels

```
error, warn, info, verbose, debug, silly
```

### 