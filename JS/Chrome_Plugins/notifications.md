# Notifications

Need `notifications` permission in manifest.json

```js
  const notif = await browser.notifications.create({
    type: "basic",
    title: "HI Mother",
    message: "Folder fff",
    iconUrl: "../img/logo.png"
  });
```

### Listening for Click

```js
async function handleC(clickedNotif) {
  if (clickedNotif === notif_id) {
    debug("THEY CLICKED ON MY BABY");
browser.notifications.onClicked.removeListener(handleC);
    await browser.notifications.clear(notif_id); 
    //close after click
  }
}
browser.notifications.onClicked.addListener(handleC);
```

## Old Way

This has better error messages and will tell you what is missing

All these fields are **required** for notification create

```js
chrome.notifications.create(
  {
    type: "basic",
    title: "HI",
    message: `Folder`,
    iconUrl: "../img/logo.png"
  },
  notif_id => {
    console.log("Created", notif_id);
  }
);
```

