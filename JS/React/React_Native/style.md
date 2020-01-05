# Style

- Pass in style object into style prop
- Can pass in an array and the last in array will override/cascade like CSS

```jsx
import { Button, StyleSheet, View } from 'react-native';
const styles = StyleSheet.create({
  container: {
   flex: 1,
   justifyContent: 'center',
  },
  buttonContainer: {
    margin: 20
  },
  alternativeLayoutButtonContainer: {
    margin: 20,
    flexDirection: 'row',
    justifyContent: 'space-between'
  }
});

//....
<View style={styles.container}>
  <View style={styles.buttonContainer}>
    //.......
  </View>
</View>
//....
```

## Layouts

### Absolute

Can use `position: absolute` with top, right, bottom, and left

### Flex

Parent element should have a width/height/flex defined or its size will be 0 and everything wont exist

Set `flex:1` to tell View to expand to fit available space, different numbers mean take up that ratio of space compared to neighbors

Change `flexdirection` to row to do within that view

`justifyContent` => main-axis alignment like flex box

[`alignItems`](https://facebook.github.io/react-native/docs/layout-props#alignitems) => cross-axis, `stretch` is default value

```jsx
export default function FlexBasics() {
    return (
      // Try setting `flexDirection` to `column`.
      <View style={{flex: 1, flexDirection: 'row'}}>
        <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'skyblue'}} />
        <View style={{width: 50, height: 50, backgroundColor: 'steelblue'}} />
      </View>
    );
  }
};
```

#### Parent Styles

`flexGrow` => default flex grow of children

`flexShrink` => default flex shrink of children

`flexBasis` => default size along main axis of children

## Platform Specific

```jsx
 const styles = StyleSheet.create({
 	tabBarInfoContainer: {
    position: "absolute",
    bottom: 0,
    left: 0,
    right: 0,
    ...Platform.select({
      ios: {
        shadowColor: "black",
        shadowOffset: { width: 0, height: -3 },
        shadowOpacity: 0.1,
        shadowRadius: 3
      },
      android: {
        elevation: 20
      }
    })
  }
 });
```

