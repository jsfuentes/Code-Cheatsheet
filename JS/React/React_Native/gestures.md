# Gestures

## Button

```jsx
<Button
  onPress={() => {
    alert('You tapped the button!');
  }}
  title="Press Me"
  color="#841584"
/>
```

onLongPress

onPress

## Touchables

Create your own buttons with touchable

- [**TouchableHighlight**](https://facebook.github.io/react-native/docs/touchablehighlight) anywhere you would use a button or link on web. The view's background will be darkened when the user presses down on the button.
- [**TouchableNativeFeedback**](https://facebook.github.io/react-native/docs/touchablenativefeedback) on Android to display ink surface reaction ripples that respond to the user's touch.
- [**TouchableOpacity**](https://facebook.github.io/react-native/docs/touchableopacity) reduce opacity of button on click
- [**TouchableWithoutFeedback**](https://facebook.github.io/react-native/docs/touchablewithoutfeedback) handles tap without feedback

## Scrolling

[ScrollView](https://facebook.github.io/react-native/docs/scrollview)

##### Props

- pagingEnabled
-  `maximumZoomScale` and `minimumZoomScale` props use gestures to zoom in and out

```jsx
import React, { Component } from 'react';
import { ScrollView, Image, Text } from 'react-native';

export default class IScrolledDownAndWhatHappenedNextShockedMe extends Component {
  render() {
      return (
        <ScrollView>
          <Text style={{fontSize:96}}>Scroll me plz</Text>
          <Image source={{uri: "https://facebook.github.io/react-native/img/tiny_logo.png", width: 64, height: 64}} />
        </ScrollView>
      );
  }
}
```

