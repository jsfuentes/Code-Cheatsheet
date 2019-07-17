# Content Scripts

By default, runs after page has loaded

Cant access most chrome apis, but communicates with messages

## Settings

```json
  "content_scripts": [
    {
      "matches": ["http://*.nytimes.com/*"],
      "run_at": "document_idle",
      "js": ["contentScript.js"]
    }
  ],
```

##### Run_at

- `document_idle` ( **default**) - Guaranted to run after DOM is loaded so no needed to wait for window.onload
- `document_start` - after css, but before any DOM or script is run
- `document_end` - immediately after DOM is complete, but before subresources like images and frames have loaded

There is fancy matching settings and white and black lists