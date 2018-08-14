# ES6 Specific Features

## Computed Property Names

```js
//ES6
var a = {
  [name]: value
});

//ES5
var a = {};
partialState[name] = value;
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

