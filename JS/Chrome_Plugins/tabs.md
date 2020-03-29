# Tabs

### Open New Tab

```js
const createProperties = { url: `localhost:3000/show/${show_id}/edit` };
browser.tabs
  .create(createProperties)
  .catch(err => console.error("Tab create error: ", err));
```

### Get active tab

```js
const queryInfo = {
  lastFocusedWindow: true,
  active: true
};
browser.tabs.query(queryInfo).then(tabs => {
  const activeTab = tabs[0];
});
```

### Send Message to All Tabs

```js
browser.tabs.query({}, (tabs) => {
  const msg = 
  tabs.forEach(tab => {
	        chrome.tabs.sendMessage(tabs[i].id, message);
  })
}); //untested
```