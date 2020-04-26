# Shortcuts / Commands

background listener

```js
 chrome.commands.onCommand.addListener(function(command) {
        console.log('Command:', command);
      });
```

manifest.json

```json
      {
        "name": "My extension",
        ...
        "commands": {
          "toggle-feature-foo": {
            "suggested_key": {
              "default": "Ctrl+Shift+Y",
              "mac": "Command+Shift+Y"
            },
            "description": "Toggle feature foo"
          },
          "_execute_browser_action": {
            "suggested_key": {
              "windows": "Ctrl+Shift+Y",
              "mac": "Command+Shift+Y",
              "chromeos": "Ctrl+Shift+U",
              "linux": "Ctrl+Shift+J"
            }
          },
          "_execute_page_action": {
            "suggested_key": {
              "default": "Ctrl+Shift+E",
              "windows": "Alt+Shift+P",
              "mac": "Alt+Shift+P"
            }
          }
        },
        ...
      }
```

