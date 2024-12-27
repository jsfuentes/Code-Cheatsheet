# Orientation

```ts
import * as ScreenOrientation from 'expo-screen-orientation';

//...
  useEffect(() => {
    //lock screen orientation to portrait
    (async () => {
      await ScreenOrientation.lockAsync(ScreenOrientation.OrientationLock.PORTRAIT);
    })();
  }, []);
```

