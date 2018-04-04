# Javascript

## Objects
Everything is an object `{}`, dictionaries are objects.
To iterate over object:
```js
for (var pId in players) {
   if (players.hasOwnProperty(pId)) {
```

## errors
try {
    Block of code to try
}
catch(err) {
    Block of code to handle errors
}


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
