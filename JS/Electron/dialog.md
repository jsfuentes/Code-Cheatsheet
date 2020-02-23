# Dialog

Show blocking native messages

```js
const indexOfClickedButton = dialog.showMessageBoxSync({
  type: "warning",
  message: "Welcome to the future",
  title: "Permissions Error"
});
console.log("Printed after the message is accepted")
```

