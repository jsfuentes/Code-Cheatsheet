# SafeArea

Because of notches and shit, you have to handle the weird layout issues

```react
import { SafeAreaProvider } from 'react-native-safe-area-context';

function App() {
  return <SafeAreaProvider>...</SafeAreaProvider>;
}

import { SafeAreaView } from 'react-native-safe-area-context';
import {StatusBar} from 'react-native';

function SomeComponent() {
  return (
    <SafeAreaView style={{ flex: 1, backgroundColor: 'red' }} edges={['right', 'top', 'left']}>
      <StatusBar barStyle='dark-content' />
      <View style={{ flex: 1, backgroundColor: 'blue' }} />
    </SafeAreaView>
  );
}
```

There are [several](https://stackoverflow.com/questions/61887661/what-are-the-differences-between-different-implementations-of-safeareaview) different SafeAreaViews. The default one from 'react-native' is pretty good, but leaves white space at the top and bottom of notches iPhones. Instead the one from 'react-native-safe-context' lets you ignore it for the bottom.