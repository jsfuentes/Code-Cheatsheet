# Built-in Components

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

### [ScrollView](https://facebook.github.io/react-native/docs/scrollview)

- generic scrolling container that can contain multiple components and views
- can scroll both vertically and horizontally (by setting the `horizontal` property).
- can allow paging through views using swiping gestures by using the `pagingEnabled` props(can also use [ViewPager](https://github.com/react-native-community/react-native-viewpager)  for horizontal swipes on Android) 
- On iOS, ScrollView with a single item could setup pinch to zoom with `maximumZoomScale` and `minimumZoomScale`
- Renders everything in ScrollView, use List Views if many many items

### List Views

#### FlatList

Scrolling list of changes of similarly structured data that doesn't prerender everything

```jsx
<View style={styles.container}>
  <FlatList
    data={[
      {key: 'John'}, //need keky for each item
      {key: 'Jimmy'},
      {key: 'Jorge'}
    ]}
    renderItem={({item}) => <Text style={styles.item}>{item.key}</Text>}
    />
</View>
```

#### SectionList

Renders set of data broken into logical sections

```jsx
<SectionList
  sections={[
    {title: 'D', data: ['Devin', 'Dan', 'Dominic']},
    {title: 'J', data: ['Jackson', 'James', 'Jillian']}
  ]}
  renderItem={({item}) => <Text style={styles.item}>{item}</Text>}
  renderSectionHeader={({section}) => <Text style={styles.sectionHeader}>{section.title}</Text>}
  keyExtractor={(item, index) => index}
  />
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
