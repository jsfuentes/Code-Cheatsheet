# Array

## basics

```javascript
var fruits = ['Apple', 'Banana'];

var last = fruits[fruits.length - 1];
```

- `.push(e)` 
- `.pop()`
- `.shift()` - popleft returning first ale
- `.indexOf(e)` - return index of ele or -1

## Functional Stuff

- `.map(ft)` - return new array with ft applied to each
- `.reduce(ft)` - return single ele..
- `.some(ft)` - true if one ele satisfies ft given

## Advanced

### Subarr

-`.slice` for subarrs 

`.splice([start index], [number beyond start]) for removing&saving section

```javascript
var removedItem = fruits.splice(pos, 1); // this is how to remove a single item at pos
```

### copy

```javascript
var fruitCopy = fruits.slice(); 
```

### For each

Executes a callback ft for each ele, returns undefined

```js
array1.forEach(function(element) {
  console.log(element);
});
```

