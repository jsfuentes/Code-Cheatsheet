# ES6 Specific Features

## Spread

expand an array to serve as args/eles for another ft 

```javascript
function myFunction(x, y, z) { }
var args = [0, 1, 2];
myFunction.apply(null, args);
//becomes
function myFunction(x, y, z) { }
var args = [0, 1, 2];
myFunction(...args);
```

#### Other uses

```javascript
var arr2 = [...arr]; // like arr.slice()

<Component {...this.props} more="values" /> //React
    
var parts = ['shoulders', 'knees']; 
var lyrics = ['head', ...parts, 'and', 'toes'];

var obj1 = { foo: 'bar', x: 42 };
var obj2 = { foo: 'baz', y: 13 };
var clonedObj = { ...obj1 };
// Object { foo: "bar", x: 42 }
var mergedObj = { ...obj1, ...obj2 };
// Object { foo: "baz", x: 42, y: 13 }
```

## Computed Property Names

```js
name = "hi"
//ES6
var a = {
  [name]: value
});

//ES5
var a = {};
a[name] = value;
```

More complex example

```js
var i = 0;
var a = {
  ['foo' + ++i]: i,
  ['foo' + ++i]: i
};

console.log(a.foo1); // 1
console.log(a.foo2); // 2
```

## Arrow functions

Preserves this function

```js
e => {

}
```

