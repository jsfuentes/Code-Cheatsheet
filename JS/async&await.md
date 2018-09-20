# Async and Await

Builds off of promises and very similar to python's asyncio

```javascript
async function catFetch(userId) {
    const response = await fetch('....')
    return await response.json();
}
```

Async functions return a promise and let you use await whihc waits on promises

If the awaiting(only one await at a time) is limiting you can always fall back on promises

