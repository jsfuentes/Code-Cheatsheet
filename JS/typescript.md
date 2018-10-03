# TypeScript
A superscript of javascript that is transpiled into javascript. Even if an error, will compile to javascript. I.e using the wrong type for a variable will produce compile error, but produce working js
New:

* Strong Typing
* Object oriented
* Compile time errors

`let` introduces scoping to {} blocks like for loops(also in ES6(2015))

```ts
let a: number;
let b: boolean;
let c: string;
let d: any;
let e: number[] = [1,2,3];
let f: any[] = [1, true, 'a'];

enum Color { Red = 0, Green = 1, Blue = 2};
let backgroundColor = Color.Red;
```

By default the type is any.
To use as a type, `(message as string)` purely a way to tell Typescript compiler what it is(and intelligent IDEs)

When you define and assign value, type is autoinferred

### Classes
```ts
interface Point {
  x: number,
  y: number
}

class Point {
  x:number;
  private y:number;
  draw() {
    console.log(this.x);
  }
  constructor(x:number, y:number){
    this.x = x;
    this.y = y;
  }
}

let point = new Point(1, 2);
point.draw();
point.x;
```
Everything public, but use private when you need it

Can autogenerate fields and set it properly just by defining it in the constructor with private/public.  
```ts
class Point {
  draw() {
    console.log(this.x);
  }
  constructor(private x:number, private y:number){ }
}
```


#### Properties
Simplify syntax, dont need both get and set.
```ts
class Point {
  constructor(private _x:number, private _y:number){ }

  get x() {
    return this._x;
  }

  set x(value) {
    // checking and setting
  }
}

let point = new Point(1, 2);
let x = point.x;
point.x = 10;
```


### Optional Parameters
Can't have multiple constructors or functions with different type definitions, so adding a question mark after a parameter makes it optional

```ts
class Point{
  //...
  constructor(x?: number, y?: number)
}
```

Everything after the first optional parameter should be optional too

### Modules
Export keyword make this a module that can be imported

```ts
//In point.ts
export class Point {
  //...
}

//OTHER file in same dir
import { Point } from ./point
```

