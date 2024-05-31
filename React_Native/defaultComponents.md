# Built-in Components

See listViews.md for all the lists `ScrollView`, `FlatList`, and  `SectionList` 

```jsx
import {
  Image,
  ScrollView, //view with scroll
  View, //like <div> or <span>
  Text, //must be used for strings
  FlatList,
  
  //See Gestures v
  Button,
  TouchableOpacity
} from "react-native";
```

### Image

```jsx
function BananaImage() {  
	let pic = { 
    uri: 'https://upload.wikimedia.org/wikipedia/commons/d/de/Bananavarieties.jpg' 
  };

  return (
    <Image source={pic} style={{width: 193, height: 110}}/>
  );
}
```

### Text Input

```jsx
function PizzaTranslator() {
  const [text, setText] = useState("");

  return (
    <TextInput
      style={{ height: 40 }}
      placeholder="Type here to translate!"
      onChangeText={setText}
      value={text}
      />
  );
}
```

### Alert

```ts
  const createTwoButtonAlert = () =>
    Alert.alert('Alert Title', 'My Alert Msg', [
      {
        text: 'Cancel',
        onPress: () => console.log('Cancel Pressed'),
        style: 'cancel',
      },
      {text: 'OK', onPress: () => console.log('OK Pressed')},
    ]);
```

