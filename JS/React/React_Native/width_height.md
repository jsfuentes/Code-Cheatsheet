# Dimensions

- Unitless in React-Native and represent density-independent pixels

```jsx
  <View>
    <View style={{width: 50, height: 50, backgroundColor: 'powderblue'}} />
    <View style={{width: 100, height: 100, backgroundColor: 'skyblue'}} />
    <View style={{width: 150, height: 150, backgroundColor: 'steelblue'}} />
  </View>
```

### Width and Height

Both `width` and `height` can take following values:

- `auto` => default based on its content
- `pixels` => absolute pixels, could change b/c of other styles
- `percentage` => % of parent