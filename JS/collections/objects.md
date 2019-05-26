# Objects

Dicts are objects, access members with ['name'] or .name

```js
var person = {}; //{} 
var person1 = new Object();
```

## Iterate Over

```js
for (var pId in players) {
   if (players.hasOwnProperty(pId)) {
       
for (..... ) {
	Object.keys(players)[0]
}
```

## General 

#### Check in

```javascript
'x' in {'x': 1} //true
```

#### Combine Objects

```javascript
Object.assign(x, y, z) //objects on the right override those to the left
```

#### Copy

```js
Object.assign({}, x)
```

#### Delete

```js
delete myObject.prop;
```

## Old Classes

```js
function Person(name) {
  this.name = name;
  this.greeting = function() {
    alert('Hi! I\'m ' + this.name + '.');
  };
}

var person1 = new Person('Bob'); //new returns obj
var person2 = new Person('John'); //contains a new definition of gretting
```

To define functions out of scope, 

```js
function Test(a, b, c, d) {
  // property definitions
}

// First method definition
Test.prototype.x = function() { ... };

// Second method definition
Test.prototype.y = function() { ... };
```



Can always add new values

```js
person1.newv = "secretsss";
```

## Prototypes?

objects can have a **prototype object** that all instances inherit from, everyone inherits from object prototype

```js
Person.prototype
Object.prototype
```

Changes to prototype affect all people

```js
Person.prototype.farewell = function() {
  alert(this.name.first + ' has left. Bye for now!');
};
person1.farewell();
```

## Create

`Object.create` makes a new object with the object given as its prototype, basically defining a subclass

```js
var person3 = Object.create(person1);//copy constructor, (inherit from person1)
```

## Inheritance

Its a mess, stupid javascript didn't want to do this 

```js
function Teacher(first, last, age, gender, interests, subject) {
    Teacher.prototype = Object.create(Person.prototype); //inherit from Person.prototype
    Teacher.prototype.constructor = Teacher; //you just replaced the constructor, add it back
    Person.call(this, first, last, age, gender, interests); //.call allows you to pass this setting it

  this.subject = subject;
}
```

