# Manifest

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
  "options_page": "options.html",

  "background": {
    "scripts": ["build/background.js"]
    "type": "module"
    //type module means import as ES module, remove line so regular script
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

Then go to `chrome://extensions` and click load unpacked extensions and click the folder of your code.

Boom, chrome extension. Click reload on changes.

### Use React/Import/ES6 in Plugins

Use a bundler like webpack or parcel and output a single js file that you include as the script in some build folder

```json
{
  "name": "chrome-base",
  "version": "0.1.0",
  "description": "Make web social again",
  "main": "scripts/scripts/js/main.js",
  "scripts": {
    "build:content": "parcel build scripts/content/content.js -d dist/build/ -o content.js",
    "watch:content": "parcel watch --no-hmr scripts/content/content.js -d dist/build/ -o content.js",
    "build:background": "parcel build scripts/background/background.js -d dist/build/ -o background.js",
    "watch:background": "parcel watch --no-hmr scripts/background/background.js -d dist/build/ -o background.js",
    "build": "concurrently \"npm run build:content\" \"npm run build:background\"",
    "watch": "concurrently \"npm run watch:content\" \"npm run watch:background\"",
    "clean": "rm -rf node_modules && rm package-lock.json"
  },
  "author": "Jorge Fuentes",
  "dependencies": {
    "@babel/runtime": "^7.5.5",
    "debug": "^4.1.1",
    "parcel-bundler": "^1.12.3",
    "react": "^16.8.6",
    "react-dom": "^16.8.6"
  },
  "devDependencies": {
    "@babel/core": "^7.6.2",
    "@babel/plugin-transform-runtime": "^7.6.2",
    "@babel/preset-env": "^7.6.2",
    "@babel/preset-react": "^7.0.0",
    "concurrently": "^4.1.0",
    "eslint": "^6.6.0",
    "eslint-config-prettier": "^6.5.0",
    "eslint-plugin-prettier": "^3.1.1",
    "eslint-plugin-react": "^7.16.0",
    "eslint-plugin-react-hooks": "^2.2.0",
    "prettier": "^1.18.2",
    "webextension-polyfill": "^0.5.0"
  }
}
```

Then change manifest.json to have the build scripts

Make sure all the files you want are imported in the one file you build

#### Content Security Policy

Not allowed to load external scripts in manifest V3

```json
"content_security_policy": "script-src 'self' https://example.com; object-src 'self'"
```

