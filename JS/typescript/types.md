# Types

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

## Objects

As we’ve seen, they can be anonymous:

```ts
function hi(person: { name: string; age: number }) {
  return "Hello " + person.age;
}
```

or they can be named by using either an **interface**(for object shapes, can be extended/implemented)

```ts
interface Person {
  name: string;
  age: number;
}

function greet(person: Person) {
  return "Hello " + person.age;
}
```

or a type alias(unions, primitive,tuple, intersection, etc)

```ts
type Person = {
  name: string;
  age: number;
};

function greet(person: Person) {
  return "Hello " + person.age;
}
```

### Extends

Interfaces only

```ts
class Car {
  printCar = () => {
    console.log("this is my car")
  }
};

interface NewCar extends Car {
  name: string;
};

class NewestCar implements NewCar {
  name: "Car";
  constructor(engine:string) {
    this.name = name
  }
  printCar = () => {
    console.log("this is my car")
  }
};
```

### Union

```ts
interface UpdateAction {
  type: CallStateActionTypes.UPDATE_LAYER,
  receiveSettings: RecieveSettings
}
interface SwapAction {
  type: CallStateActionTypes.SWAP_POSITION,
  id1: string,
  id2: string,
}

type CallStateActions = UpdateAction|SwapAction;
```

#### Intersection

```ts
interface Name {
  name: “string”
};

interface Age {
  age: number
};

type Person = Name & Age;
```

#### Tuples

Array of fixed size that can have different known types 

```ts
type Reponse = [string, number]

function maxHeightWidth(
  ratio: number,
  maxWidth: number,
  maxHeight: number
): [width: number, height: number] 
```

#### Any vs unknown

**Use unknown** as it blocks fields unless narrowed, as any lets you do untypesafe things

#### Never

Never is the empty set and will never have a value

```typescript
function timeout(ms: number): Promise<never> {
  return new Promise((_, reject) =>
    setTimeout(() => reject(new Error("Timeout elapsed")), ms)
  )
}

//useful because will only be return type of fetchStock as T | never = T
const stock = await Promise.race([
  fetchStock(tickerSymbol),
  timeout(3000)
])
```

## Functions

#### Generics

```ts
function firstElement<Type>(arr: Type[]): Type | undefined {
  return arr[0];
}
```

## Advanced

```typescript
type NonNullable<T> = T extends null | undefined ? never : T;
```

This works because conditional types [distribute](https://www.typescriptlang.org/docs/handbook/advanced-types.html#distributive-conditional-types) over type unions. Given any type of the form `T extends U ? X : Y` when a union type is substituted for `T` the type expands to distribute the condition to each branch of that union type: