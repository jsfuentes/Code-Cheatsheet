# React Native

- Every [core component](https://reactnative.dev/docs/components-and-apis) is different and native, but uses React syntax like View, Text, ScrollView, Button, Modal
- Stylesheets are pretty similar, but every View is automatically in a flexbox already

Try out in browser with [Snack](https://snack.expo.io/)

Check out [resources](http://www.awesome-react-native.com/)

## Web Browsers

```jsx
import * as WebBrowser from "expo-web-browser";

function handleLearnMorePress() {
  WebBrowser.openBrowserAsync(    "https://docs.expo.io/versions/latest/workflow/development-mode/"
  );
}

 	//......
  return (
    <Text onPress={handleLearnMorePress} style={styles.helpLinkText}>
      Learn more
    </Text>
  );
```

## Globals

`__DEV__` => true if React Native in dev mode

```jsx
import { Platform } from "react-native";

if(Platform.OS === "ios") 
  //...

const config = Platform.select({
  web: { headerMode: "screen" },
  default: {}
});
```

