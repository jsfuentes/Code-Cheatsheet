# Promises

```ts
let promiseToClean = new Promise(function(resolve, reject) {
    let isClean = true;
    if(isClean){
      resolve('Clean');
    } else {
      reject('Not Clean');
    }
  });

//when promise is resolved
promiseToCleanTheRoom.then((fromResolve) => {
  console.log('the room is' + fromResolve);
}).catch( (fromReject) => {
  console.log('the room is' + fromReject);
}));
```

## Promisify

```javascript
function screenshotPromise(windowId) {
  return new Promise((resolve, reject) => {
    chrome.tabs.captureVisibleTab(windowId, {quality: 10},
      (screenshotData) => {
        console.log("Screenshot", screenshotData);
        resolve(screenshotData);
      });
  });
}
```

## PROMISE ALL

```ts
var promise1 = Promise.resolve(3);
var promise2 = 42;
var promise3 = new Promise(function(resolve, reject) {
  setTimeout(resolve, 100, 'foo');
});

Promise.all([promise1, promise2, promise3]).then(function(values) {
  console.log(values);
});
// expected output: Array [3, 42, "foo"]
```

### RETURNING IN then
When you return something from a then() callback, it's a bit magic. If you return a value, the next then() is called with that value. However, if you return something promise-like, the next then() waits on it, and is only called when that promise settles (succeeds/fails).

```ts
getJSON('story.json').then(function(story) {
  return getJSON(story.chapterUrls[0]);
}).then(function(chapter1) {
  console.log("Got chapter 1!", chapter1);
})
```
