# [Development Build](https://docs.expo.dev/develop/development-builds/introduction/)

Basically like your own version of Expo Go that you install on your device

In `eas.json`, add development client true and distribution internal

eas.json

```json
{
  "build": {
    "development": {
      "developmentClient": true,
      "distribution": "internal"
    },
    "preview": {
      "distribution": "internal"
    },
    "production": {}
  }
}
```

