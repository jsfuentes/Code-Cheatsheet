# Fluxible

A less popular version of redux made by Yahoo, remember flux is a design pattern and fluxible and redux are implementations

## Connect to Stores

```jsx
Component = connectToStores(Component, [FooStore, BarStore], (context, props) => ({
    foo: context.getStore(FooStore).getFoo(),
    bar: context.getStore(BarStore).getBar()
}));
```

