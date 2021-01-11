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
function greet(person: { name: string; age: number }) {
  return "Hello " + person.age;
}Try
```

or they can be named by using either an interface

```ts
interface Person {
  name: string;
  age: number;
}

function greet(person: Person) {
  return "Hello " + person.age;
}
```

or a type alias.

```ts
type Person = {
  name: string;
  age: number;
};

function greet(person: Person) {
  return "Hello " + person.age;
}
```

## React Proptypes

Prop types:

```js
MyComponent.propTypes = {
  error: PropTypes.instanceOf(Error),
  children: PropTypes.node,
  status: PropTypes.oneOf(['inactive', 'inProgress', 'success', 'failed'])
  value: PropTypes.oneOfType([
    PropTypes.string,
    PropTypes.number,
    PropTypes.instanceOf(Error)
  ]),
}
```

TypeScript:

```ts
interface Props {
  error: Error
  children: React.ReactNode
  status: 'inactive' | 'inProgress' | 'success' | 'failed'
  value: string | number | Error
}
```