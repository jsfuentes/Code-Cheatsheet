# Async and Await

ES6, builds off of promises and very similar to python's asyncio

```javascript
async function catFetch(userId) {
    const response = await fetch('....')
    return await response.json();
}
```

Async functions return a promise and let you use await whihc waits on promises

If the awaiting(only one await at a time) is limiting you can always fall back on promises


### Wait with 

```js
function delay(timeout) {
  return new Promise((resolve) => {
    setTimeout(resolve, timeout);
  });
}
async function ... {
    ....
	await delay(3000);
}
```

## Async Ft == Promise

```javascript
async function main () {
    //....
}

main()
  .then(() => console.log("COMPLETE"))
  .catch(console.error);
```

### Can just use async functions in a promise

```js
configPromise.then(async (econfig) => {
  debug("Econfig", econfig);
  const test = await updateStorage(econfig);
});

new Promise(async (resolve, reject) => {
  const result = await browser.management.getSelf();
  //..
```

*Look at babel runtime to get in the browser*