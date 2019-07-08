# Debugging

Great playground in chrome console 

### Most common errors

1. Thinking the value is invalid when it is actually undefined
2. Not awaiting for a promise
3. Can't do await in map/filter ft

## Console

```javascript
console.log( { x }); //{ } prints it as a dict so you get the variable name
console.table([1, 2]); // log in table 
console.trace('hi'): //will do stack trace

//Can compute performace
console.time("looper");
//some op
console.timeEnd("looper"); //=> looper: 4.3ms
```

### Is something you are requiring undefined?

- Circular dependency, module.exports will just return null

