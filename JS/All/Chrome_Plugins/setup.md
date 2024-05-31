# Setup

## Min Chrome Plugin

manifest.json

```json
{
  "manifest_version": 3,
  "name": "Hello Extensions",
  "description": "Base Level Extension",
  "version": "1.0",
  "action": {
    "default_popup": "hello.html",
    "default_icon": "hello_extensions.png"
  }
}
```

hello.html

```html
<html>
  <body>
    <h1>Hello Extensions</h1>
  </body>
</html>
```

### [Load unpacked extension](https://developer.chrome.com/docs/extensions/get-started/tutorial/hello-world#load-unpacked)

1. Go to `chrome://extensions`
2. Click load unpacked and select extension directory

- Now when you make changes click the reload button for that plugin in `chrome://extensions`