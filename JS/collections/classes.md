# Classes

ES6, Syntacical sugar actually just doing object prototyping

Extended by typescript, see that section

```js
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
  // Getter
  get area() {
    return this.calcArea();
  }
  // Method
  calcArea() {
    return this.height * this.width;
  }
  //static
  static distance(a, b) {
    const dx = a.x - b.x;
    const dy = a.y - b.y;

    return Math.hypot(dx, dy);
  }
}

const square = new Rectangle(10, 10);

console.log(square.area); // 100
```

## Inheritance

Subclasses must `super()`

```js
class Teacher extends Person {
  constructor(first, last, age, gender, interests, subject, grade) {
    super(first, last, age, gender, interests);

    // subject and grade are specific to Teacher
    this.subject = subject;
    this.grade = grade;
  }
}
```

## Interfaces

Hhahahha, did you think this was a good language?!? 

Just use class 