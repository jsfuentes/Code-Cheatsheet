# Clipboard

## NPM Pakcage

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

## Old

- `document.execCommand("copy")`
- `document.execCommand("cut")`
- `document.execCommand("paste")`



## Modern Way

Experimential

```
navigator.clipboard.readText().then(text => outputElem.innerText = text);

```

