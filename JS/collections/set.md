# Set

```js
const set1 = new Set([1, 2, 3, 4, 5]);
set1.has(1); // expected output: true
set1.add(2);
set1.delete(2);
set1.clear();
set1.size;
```

### Convert to Array

`Array.from(set1)`

## Set Operations

```js
let union = new Set([...a, ...b]);
let intersection = new Set([...a].filter((x) => b.has(x)));
let difference = new Set([...a].filter((x) => !b.has(x)));
```
