# Map

In general, dont use unless you need nonstring keys or insertion order

## Overview
 `Map()` is funcitonally equivalent to objects but:

- Provides `get`, `set`, `has`, `delete`, and `size` methods.

- **Accepts any type for the keys** instead of just strings.

- Provides an iterator for easy `for-of` usage and **maintains the order of results.**

- Doesn't have edge cases with prototypes and other properties showing up during iteration or copying.

- Slower than just objects, b/c [js engines compile objects to C++](https://mathiasbynens.be/notes/shapes-ics)

- Maps can be bigger than objects (16.7M vs 11.1M in Chrome)

- Can be more cumbersome than objects

  - ```js
    obj[key] += x	
    //vs
    map.set(map.get(key) + x)
    ```

  - Harder to debug in console

## Usage

```js
const myMap = new Map();

const keyString = 'a string',
    keyObj = {},
    keyFunc = function() {};

// setting the values
myMap.set(keyString, "value associated with 'a string'");
myMap.set(keyObj, 'value associated with keyObj');
myMap.set(keyFunc, 'value associated with keyFunc');

console.log(myMap.size); // 3

// getting the values
console.log(myMap.get(keyString));    
// "value associated with 'a string'"
console.log(myMap.get(keyObj));       
// "value associated with keyObj"
console.log(myMap.get(keyFunc));      
// "value associated with keyFunc"

console.log(myMap.get('a string'));   
// "value associated with 'a string'"
// because keyString === 'a string'
console.log(myMap.get({}));          
// undefined, because keyObj !== {}
console.log(myMap.get(function() {})) 
// undefined, because keyFunc !== function () {}
```

