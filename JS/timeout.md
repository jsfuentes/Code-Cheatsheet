# Timeout

```javascript
if(this.timerID !== undefined) {
  clearTimeout(this.timerID);
}
this.timerID = setTimeout(this.sendPayload, 4000);
```

## Interval

```js
if(this.timerID !== undefined) {
	clearInterval(intervalID);
}
const intervalID = setInterval(() => alert("Hello"), 3000);

```

