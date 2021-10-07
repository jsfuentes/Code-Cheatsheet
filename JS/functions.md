#Functions

Can have default parameters, no named parameters when calling though

```js
function scrape(company, secrets, headless=false, toScrape=["All"]) {
	//...
}
```

Different ways to call ft change how it interacts with the local scope

### Using this

Use the this of the scope that defined it: `.bind(this)` or store the context `var self = this` or use arrow its

### 7 Ways to Define Ft

##### Ft Declaration

```js
function isEven(num) {
  return num % 2 === 0;
}
```

**Creates** isEven variable in current scope that hold ft obj, **hoists** ft up, and **names** it useful for debugging

Need a name for recursion

##### Arrow Ft

Takes

```javascript
const absValue = (number) => {
  if (number < 0) {
    return -number;
  }
  return number;
}
```

##### Ft Expression

```js
const isTruthy = function(value) {
  return !!value;
};
```

allows conditional setting of variable

Name informed for debugging using variable that holds it

##### Named Ft Expression

```js
const getType = function funName(variable) {
  console.log(typeof funName === 'function'); // => true
  return typeof variable;
}
```

Name only available in body, and name set as such

##### Shorthand method definition 

Possible on object literals and classes, required in classes

```js
const collection = {
  items: [],
  add(...items) {
    this.items.push(...items);
  },
  get(index) {
    return this.items[index];
  }
};
```

##### Generator Ft

```js
function* indexGenerator(){
  var index = 0;
  while(true) {
    yield index++;
  }
}
const g = indexGenerator();
console.log(g.next().value); // => 0
console.log(g.next().value); // => 1
```

Can also be used with ft expression, and method

```js
const indexGenerator = function* () {
//...
const obj = {
  *indexGenerator() {
//... 
```

###### Ft New

This is disgusting don't use, always declared in global scope

```js
const global = new Function('return this')();
```

