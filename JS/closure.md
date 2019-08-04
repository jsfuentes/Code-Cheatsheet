# Closure

Javascript has closures meaning functions defined store their environment when they are created 

```js
function makeFunc() {
  var name = 'Mozilla';
  function displayName() {
    alert(name);
  }
  return displayName;
}

var myFunc = makeFunc();
myFunc(); //Mozilla
```

Can't rely on closure for global variables 

```js
let x = 100;
let b = () => () => x;
b()(); //100
x = 10;
b()(); //10
```

This works though

```js
let x = 0;
function y() {let z = x++; return () => z}
let a = y();
let b = y();
x = 100;
a(); //0
b(); //1
```

