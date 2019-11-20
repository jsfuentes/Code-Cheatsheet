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

### [Mouse Events](https://www.w3schools.com/jquery/tryit.asp?filename=tryjquery_event_mouseenter_mouseover)

mouseover => enters the div or any of its child(div then child is twice triggered)

mouseenter => only when div first entered

 mouseleave => only when div left

onmousemove  => any movement over the div element.

## Custom Events

Use detail to hold extra information 

```js
//some event/async ft
{
  dispatchEvent(
    new CustomEvent("dance_party", {
      detail: { curId }
    });
}

addEventListener("dance_party", e => debug("Listening to ", e.detail.curId));
```

