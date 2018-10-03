# Javascript

## Control

```js
var i;
for (i = 0; i < cars.length; i++) { 
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

## Objects
Everything is an object `{}`, dictionaries are objects.
To iterate over object:
```js
for (var pId in players) {
   if (players.hasOwnProperty(pId)) {
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

```

## Date

Really untested
```js
if(era === "PM") {
  if(hour !== 12){
    hour = parseInt(hour) + 12;
  }
} else if (era === "AM") {
  if(hour === 12) {
    hour = parseInt(hour) = 0;
  }
}
```

## Other

```javascript
console.log( { x }); //{ } prints it as a dict so you get the variable name
```

