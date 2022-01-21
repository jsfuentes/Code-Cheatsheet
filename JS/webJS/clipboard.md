# Clipboard

## Old Way

Could go obsolete at some future point

- `document.execCommand("copy")`
- `document.execCommand("cut")`
- `document.execCommand("paste")`

Copies from dom so you would create an element with the text in the DOM

### Best Way

```js
export function copyToClipboard(str) {
  const el = document.createElement("textarea"); // Create a <textarea> element
  el.value = str; // Set its value to the string that you want copied
  el.setAttribute("readonly", ""); // Make it readonly to be tamper-proof
  el.style.position = "absolute";
  el.style.left = "-9999px"; // Move outside the screen to make it invisible
  document.body.appendChild(el); // Append the <textarea> element to the HTML document
  const selected =
    document.getSelection().rangeCount > 0 // Check if there is any content selected previously
      ? document.getSelection().getRangeAt(0) // Store selection if found
      : false; // Mark as false to know no selection existed before
  el.select(); // Select the <textarea> content
  document.execCommand("copy"); // Copy - only works as a result of a user action (e.g. click events)
  document.body.removeChild(el); // Remove the <textarea> element
  if (selected) {
    // If a selection existed before copying
    document.getSelection().removeAllRanges(); // Unselect everything on the HTML document
    document.getSelection().addRange(selected); // Restore the original selection
  }
}
```

## Option 2(No Safari)

```js
function copyToClipboard(str, mimeType = "text") {
  return new Promise(resolve => {
    const old = document.oncopy;
    document.oncopy = event => {
      event.clipboardData.setData(mimeType, str);
      event.preventDefault();
      document.oncopy = old;
      resolve();
    };
    document.execCommand("copy", false, null);
  });
}
```

## Modern Way

[Only supported in Chrome since mid 2019 and 2020 Edge](https://caniuse.com/#search=clipboard API)

Experimential

```
navigator.clipboard.readText().then(text => outputElem.innerText = text);
```

The page is required to be active (doesn't work in console)

*Has so many security concerns like request permissions from user, blehhhhh don't use*

## NPM Package?

```bash
npm i clipboard --save
```

```js
import ClipBoard from 'clipboard';
console.log(ClipBoard);
new ClipboardJS('.btn');
```

```html
<!-- Target -->
<input id="foo" value="https://github.com/zenorocha/clipboard.js.git">

<!-- Trigger -->
<button class="btn" data-clipboard-target="#foo">
    <img src="assets/clippy.svg" alt="Copy to clipboard">
</button>
```

