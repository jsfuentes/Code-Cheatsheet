# Browser Action

```js
await browser.browserAction.setBadgeBackgroundColor({
  color: "#000000"
});

await browser.browserAction.setBadgeText({
  text: number.toString()
});
```

If badge text set to "", then the badge completely disappears regardless of teh badge color