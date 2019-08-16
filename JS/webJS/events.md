# Events

Two ways to interact: 

- generalized [`addEventListener()`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) 
  - Ex: `e.addEventListener('click', handleClick);`
- specific on-<event> handlers
  - **only one** *on-event* handler for a given event
  - Ex: `e.onclick = handleClick`
  - Call with  `e.onclick()`
  - Print current function `e.onclick.toString()`

**load** | **click** | blur | error | focus | scroll | mouseover | keydown

```js
document.body.onload = () => { .... };
```

Event handlers take an event parameter

### Remove Listener

Must have same arguments, so can't do anonoymous ft

```js
clickTarget.addEventListener('click', handleer)
clickTarget.removeEventListener('click', handleer)
```

Just overwrite ez

```js
e.onclick = () => alert('hi');
e.onclick = () => alert('bye');
```

###HTML

```html
<button onclick="return handleClick(event);">
```

