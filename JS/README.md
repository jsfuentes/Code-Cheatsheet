# Javascript

`"use strict";` at the top of files will prompt new compliers to throw more errors like for using undefined variables

## Control

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

## Errors

```javascript
try {
  // Block of code to try
  throw "Parameter is not a number!";
  //throw new Error([message[, fileName[, lineNumber]]])
}
catch(err) {
  // Block of code to handle errors
}
```

```js
throw new Error("This is an error");
```

*Can throw anything actually but don't*

## Date

Can get and set different aspects and convert to different types

```js
var x = new Date(); //get current date
x.toDateString(); //=> "Fri Oct 05 2018"
x.toISOString(); //=> "2018-12-31T03:21:15.934Z"
```

## Functions

Can have default parameters, no named parameters when calling though

```js
function scrape(company, secrets, headless=false, toScrape=["All"]) {
	//...
}
```

## Equality

`===` is strict equality with type and strict

```javascript
77 === '77'
// false (Number v. String)
```

`==`  uses type coercion 

```javascript
77 == '77'
// true
```

## Type Conversion

```js
1.toString() //='1'
parseInt('42', 10) //42
parseInt('42px', 10) //42
parseInt('10a,a22') //10
```

Find type with `typeof(var)`