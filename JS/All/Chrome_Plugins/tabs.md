# Tabs

Mostly don't need `tabs` permission, except to populate `url`, `pendingUrl`, `title`, and `favIconUrl` properties of `Tab`.

### Open New Tab

```js
const createProperties = { url: `localhost:3000/show/${show_id}/edit` };
browser.tabs
  .create(createProperties)
  .catch(err => console.error("Tab create error: ", err));
```

### Get active tab

```js
const tabs = await browser.tabs.query({
  lastFocusedWindow: true,
  active: true
});
const activeTab = tabs[0];
```

### Send Message to All Tabs

```js
browser.tabs.query({}).then((tabs) => {
  tabs.forEach((tab) => {
    ensureValidContent(tab.id).catch(console.error);
  });
});
```

