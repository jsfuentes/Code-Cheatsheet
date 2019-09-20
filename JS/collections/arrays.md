# Array

## basics

```javascript
var fruits = ['Apple', 'Banana'];

var last = fruits[fruits.length - 1];
```

- `.length`
- `.push(e)` 
- `.pop()`
- `.shift()` - popleft returning first ale
- `.indexOf(e)` - return index of ele or -1
- `.includes(e)` - return true/false
- `.sort()` - Takes ft `(a,b) => `
  - < 0 — `a` b4 `b`
  - \> 0  — `b` b4 `a`
  - = 0  — `a` and `b` unchanged

## Functional Stuff

- `.map(ft)` - return new array with ft applied to each
- `flatMap(ft)` - map followed by a depth 1 [`flat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flat) , allows modification of number of elements
- `.reduce(ft)` - return single ele..
- `.some(ft)` - true if one ele satisfies ft given
- `.filter(ft)`-  return  new array with elements where ft true

```js
words.filter(word => word.length > 6);
words.map((element, index) => element+index);
arr.reduce((a,b) => a + b, 0)
```

Can do async fts in map and then wrap it in a promise.all

## Advanced

### Subarr

`.slice` for subarrs (start, end not included)

`.splice([start index], [number beyond start])` for removing&saving section

```javascript
var removedItem = fruits.splice(pos, 1); // this is how to remove a single item at pos

fruits.splice(fruits.indexOf("banana"), 1);
```

### copy

```javascript
var fruitCopy = fruits.slice(); 
```

### For each

Executes a callback ft for each ele, returns undefined

Beware async stuff

**array.forEach(callback[, thisArg])**

```js
array1.forEach(function(element) {
  console.log(element);
});
```

### Queue

- `.push(e)`

- `.pop()`
- `.shift(e)` => pop from beginning
- `.unshift()` => add to beginning