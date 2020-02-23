# Electron builder

## Mac

After 10.15 need to notarize Mac apps

Create Apple Developer Account($99), and create a Developer ID Application to sign for distribution outside the app store

#### Create Certificate Signing Request

1. Launch Keychain Access located in `/Applications/Utilities`.

2. Choose Keychain Access > Certificate Assistant > Request a Certificate from a Certificate Authority.

3. In the Certificate Assistant dialog, enter an email address in the User Email Address field.

4. In the Common Name field, enter a name for the key (for example, Gita Kumar Dev Key).

5. Leave the CA Email Address field empty.

6. Choose “Saved to disk”, and click Continue.

   ![img](https://help.apple.com/developer-account/en.lproj/Art/c_create_csr.png)

#### Add Configuration and Notarization

Must get a disposable password from Apple to use

Configure Builder as such in package.json:

```json
 "build": {
    "productName": "Slingshow",
    "appId": "org.jn.Slingshow",
    "files": [
      "assets/",
      "dist/",
      "node_modules/",
      "app.html",
      "main.prod.js",
      "main.prod.js.map",
      "package.json"
    ],
    "protocols": {
      "name": "slingshow-protocol",
      "schemes": [
        "slingshow"
      ]
    },
    "mac": {
      "hardenedRuntime": true,
      "gatekeeperAssess": false,
      "entitlements": "./configs/entitlements.mac.plist",
      "entitlementsInherit": "./configs/entitlements.mac.plist",
      "extendInfo": {
        "NSCameraUsageDescription": "This app requires camera access.",
        "NSMicrophoneUsageDescription": "This app requires microphone access."
      }
    },
    "afterSign": "./internals/scripts/afterSignHook.js",
    "dmg": {
      "contents": [
        {
          "x": 130,
          "y": 220
        },
        {
          "x": 410,
          "y": 220,
          "type": "link",
          "path": "/Applications"
        }
      ]
    },
    "win": {
      "target": [
        "nsis",
        "msi"
      ]
    },
    "linux": {
      "target": [
        "deb",
        "rpm",
        "AppImage"
      ],
      "category": "Development"
    },
    "directories": {
      "buildResources": "resources",
      "output": "release"
    },
    "publish": {
      "provider": "github",
      "owner": "jsfuentes",
      "repo": "Room",
      "private": true
    }
  },
```

afterSign.js

```js
require("dotenv").config();
const { notarize } = require("electron-notarize");

exports.default = async function notarizing() {
  try {
    if (process.platform !== "darwin") {
      console.log("Skipping notarization - not building for Mac");
      return false;
    }
    console.log("Notarizing app...");
    console.time("Notarize");
    const options = {
      appBundleId: "com.slingshow.slingshow",
      appPath:
        "/Users/jfuentes/Projects/Room/relection/release/mac/Slingshow.app",
      appleId: process.env.APPLE_ID,
      appleIdPassword: process.env.APPLE_ID_PASSWORD
    };
    if (process.env.APPLE_ID_TEAM && process.env.APPLE_ID_TEAM !== "") {
      options.ascProvider = process.env.APPLE_ID_TEAM;
    }
    await notarize(options);
    console.timeEnd("Notarize");
    console.log("Done");
    return true;
  } catch (err) {
    console.error(err);
    throw err;
  }
};

```

