# Immer

While not a redux package, it is included by default so is the langauge inside reducers

## Benefits

- No new API like Immutable.js, just use js object/arrays
- Structural sharing of unchanged parts by default
- Automatic object freezing, throws error if you try to edit(in dev)
- Strongly typed
- Very small at 3KB

## Performance

![performance graph][https://immerjs.github.io/immer/img/performance.png]

Often 3-4x slower than a handwritten reducer, but will auto not update if the state has no changes, instead of `{...x, y: 1}` which will cause anything that depends on the subfields to also rerender which is huge

## Usage

Either update the given object or return a new object

```js
state = {jklkjl: 1}  //won't work, need to edit underlying obj

return {jklkjl: 1} // return entirely new object

//BEST IMMER WAY
state.jklkjl = 1
```



