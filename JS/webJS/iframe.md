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

## Communicating Between

Inside iframe

```js
window.parent.postMessage({ type: "close_spotlight" }, "*");
```

Inside parent window

```js
window.onmessage = handlePostedQuestions;

function handlePostedQuestions(packet) {
  const msg = packet.data;
  debug("Recieved packet", packet);
  debug("Recieved msg", msg); //will be {type: ...}
}
```

## DOM

https://sites.google.com/a/chromium.org/dev/Home/chromium-security/deprecating-permissions-in-cross-origin-iframes

Deprecated Permission in Iframe unless allowed:

- Geolocation (getCurrentPosition and watchPosition)
- Midi (requestMIDIAccess)
- Encrypted media extensions (requestMediaKeySystemAccess)
- Microphone, Camera (getUserMedia)

```html
<iframe src="https://example.com" allow="geolocation,  microphone"></iframe>
```

