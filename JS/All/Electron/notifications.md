# Notifications

### Renderer

Can just use the HTML5 API in the renderer process

```jsx
function Notify() {
  function notify() {
    const myNotification = new window.Notification("HI", { body: "THERE" });
  }
  return <button onClick={notify}>Notify</button>;
}
```

### Main

```js
function callUpdateNotification() {
  const iconAddress = `file://${__dirname}/assets/logo.png`;
  const notifOptions = {
    title: "Slingshow",
    subtitle: "NOW",
    body: "Time to update your team (⌘K)",
    icon: iconAddress
  };
  const notif = new Notification(notifOptions);
  notif.show();
  notif.addListener("click", e => {
    console.log("I hear the shit out of you");
  });
}
```

Notification Options:

- title` String - A title for the notification, which will be shown at the top of the notification window when it is shown.
- `subtitle` String (optional) *macOS* - A subtitle for the notification, which will be displayed below the title.
- `body` String - The body text of the notification, which will be displayed below the title or subtitle.
- `silent` Boolean (optional) - Whether or not to emit an OS notification noise when showing the notification.
- `icon` (String | [NativeImage](https://www.electronjs.org/docs/api/native-image)) (optional) - An icon to use in the notification.
- `hasReply` Boolean (optional) *macOS* - Whether or not to add an inline reply option to the notification.
- `replyPlaceholder` String (optional) *macOS* - The placeholder to write in the inline reply input field.
- `sound` String (optional) *macOS* - The name of the sound file to play when the notification is shown.
- `actions` [NotificationAction[\]](https://www.electronjs.org/docs/api/structures/notification-action) (optional) *macOS* - Actions to add to the notification. Please read the available actions and limitations in the `NotificationAction` documentation.
- `closeButtonText` String (optional) *macOS* - A custom title for the close button of an alert. An empty string will cause the default localized text to be used.