# Iframe

Because of same-origin policy on browsers, can use javascript to access DOM elements if not from the same origin 

Message passing from iframe to window

Can use window post message or custom events dispatching

```js
if ( window.location !== window.parent.location ) {
	console.log("In iframe");
} else {
	console.log("Not in frame");
}
```

