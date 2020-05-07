# Shortcuts / Commands

Listen for key presses and get event in background script

background listener

```js
browser.commands.onCommand.addListener((command) => {
  debug("Command:", command);
  if (command === "insert-request-link") {
    insertRequestLink();
  }
});
```

manifest.json

```json
  "commands": {
    "start-recording": {
      "suggested_key": {
        "default": "Ctrl+Shift+E",
        "mac": "Command+Shift+E"
      },
      "description": "Toggle feature foo"
    }
  },
```

