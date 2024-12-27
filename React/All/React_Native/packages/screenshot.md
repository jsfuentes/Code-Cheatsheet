# React Native View Shot

```bash
npx expo install react-native-view-shot
```

## Usage

```react
function ExampleCaptureOnMountManually {
  const ref = useRef();

  useEffect(() => {
    // on mount
    ref.current.capture().then(uri => {
      console.log("do something with ", uri);
    });
  }, []);

  return (
    <ViewShot ref={ref} options={{ fileName: "Your-File-Name", format: "jpg", quality: 0.9 }}>
      <Text>...Something to rasterize...</Text>
    </ViewShot>
  );
}
```

