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

## PROMISE ALL

```ts
let cleanRoom = function() {
  return new Promise(function(resolve, reject) {
    resolve('Cleaned The Room');
  });
};

let removeGarbage = function(message) {
  return new Promise(function(resolve, reject) {
    resolve(message + ' remove Garbage');
  });
};

let winIcecream = function(message) {
  return new Promise(function(resolve, reject) {
    resolve( message + ' won Icecream');
  });
};

Promise.all([cleanRoom(), removeGarbage(), winIcecream()]).then( () => {
  console.log("all of them finished");
})
Promise.race([cleanRoom(), removeGarbage(), winIcecream()]).then( () => {
  console.log("some of them finished");
})

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
