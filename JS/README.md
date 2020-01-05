# Javascript

`"use strict";` at the top of files will prompt new compliers to throw more errors like for using undefined variables

Objects and arrays passed by reference

There are packages that work just in the browser, just in react, just for gatsby, or just for node

## Control

```js
isMember ? "$2.00" : "$10.00"

if (c) {s} else if (c) {s} else {s}
```

```js
for (let i = 0; i < cars.length; i++) { 
    text += cars[i] + "<br>";
}

switch(expression) {
    case x:
        code block
        break;
    case y:
        code block
        break;
    default:
        code block
}
```

## Equality

`===` is strict equality with type and strict

```javascript
77 === '77' // false (Number v. String)
undefined === null //false
```

`==`  uses type coercion 

```javascript
77 == '77' // true
undefined == null //true
```

## Type Conversion

```js
1.toString() //='1'
parseInt('42', 10) //42
parseInt('42px', 10) //42
parseInt('10a,a22') //10
```

Find type with `typeof(var)`

