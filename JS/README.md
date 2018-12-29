# Javascript

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
x.toDateString() //=> "Fri Oct 05 2018"
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

