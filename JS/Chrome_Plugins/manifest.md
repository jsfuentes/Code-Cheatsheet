# Manifrst

#### Permission Examples

```json
{
  "name": "Slingshow",
  "version": "0.1.0",
  "description": "Easily request and create screen videos",
  "manifest_version": 2,

  "permissions": [
    "storage",
    "identity",
    "identity.email",
    "https://sigma-fonts.s3-us-west-1.amazonaws.com/",
    "https://www.slingshow.com/",
    "http://localhost:3001/"
  ],

  "background": {
    "scripts": ["build/background.js"]
  },
  "browser_action": {
    "default_popup": "popup.html"
  },
  "icons": {
    "16": "icon16.png",
    "24": "icon24.png",
    "48": "icon48.png",
    "128": "icon128.png"
  },
  "oauth2": {
    "client_id": "575235335697-ak2b2kc8pm1j8gc9r3484h9p1thju141.apps.googleusercontent.com",
    "scopes": [
      "https://www.googleapis.com/auth/userinfo.profile",
      "https://www.googleapis.com/auth/userinfo.email"
    ]
  },
  "homepage_url": "https://www.slingshow.com",
  "web_accessible_resources": ["img/*", "fonts/*"],
  "key": "[]"
}
```



#### Content Security Policy

TO allow loading of external scripts:

```json
"content_security_policy": "script-src 'self' https://example.com; object-src 'self'"
```

