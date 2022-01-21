# Classes

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