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

## Only trigger event on parent, not children

```js
if (e.target === e.currentTarget) {
  debug("YUP");
  setIsSubChatActive(false);
}
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

#### Pointer Events [CanIUse](https://caniuse.com/#feat=pointer) 

- Allows varius inputs like touchscreens, pens, etc

- Supported in most browsers now even IE11
- In react, onPointerDown or regular pointerdown. For backwards compatability, touch/pen events fire mouse events but a little late and a little unreliably

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

