# Context Menu

Can add stuff to the right click menu

Need `"contextMenus"` permission in the manifest

background.js

```js
function searchUrbanDict(word) {
  debug("TESTING STUFF");
};

browser.contextMenus.create({
  title: "Search in UrbanDictionary",
  contexts: ["selection"], // ContextType
  onclick: searchUrbanDict, // A callback function
});
```

#### ContextTypes

`"all"`, `"page"`, `"frame"`, `"selection"`, `"link"`, `"editable"`, `"image"`, `"video"`, `"audio"`, `"launcher"`, `"browser_action"`, or `"page_action"`

#### ItemTypes

`"normal"`, `"checkbox"`, `"radio"`, or `"separator"`