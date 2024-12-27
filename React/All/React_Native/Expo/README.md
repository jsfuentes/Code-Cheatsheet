# Expo

Start a project without Xcode/Android Studio

Quickly deploy changes to your phone over ngrok, hot reloading

Expo SDK gives ez access to underlying native APIS

[Limitations](https://docs.expo.io/versions/latest/introduction/why-not-expo/) => can always eject though

**Managed** workflow has only JS and Expo does rest

**Bare** workflow give full control over native project with Expo SDK, *ejection* to regular react native project

## Constants

```js
import { Platform } from 'react-native';

if (Platform.OS !== 'web')
```

