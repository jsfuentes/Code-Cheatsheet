# JS In the Browser

Include in HTML page with 

<script src="demo_defer.js" defer></script>

## Running JS after DOM loads

`defer` like above

```js
window.onload = function() {
  init();
  doSomethingElse();
};
```

[window.onload](https://developer.mozilla.org/en-US/docs/Web/API/GlobalEventHandlers.onload)

- By default, it is fired when the entire page loads, including its content (images, css, scripts, etc.)
- In some browsers it now takes over the role of document.onload and fires when the DOM is ready as well.

document.onload

- It is called when the DOM is ready which can be prior to images and other external content is loaded.