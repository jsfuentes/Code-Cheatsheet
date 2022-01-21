# [Narrowing Types](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

Unions will cause errors if all types don't have a property

**Error**

```ts
function padLeft(padding: number | string, input: string) {
  return " ".repeat(padding) + input;
}
/*
	Argument of type 'string | number' is not assignable to parameter of type 'number'.
  Type 'string' is not assignable to type 'number'.
*/
```

**Correct**

```ts
function padLeft(padding: number | string, input: string) {
  if (typeof padding === "number") {
    return " ".repeat(padding) + input;
  }
  return padding + input;
}
```

## Guards

#### Typeof 

TypeScript expects this to return a certain set of strings:

- `"string"`
- `"number"`
- `"bigint"`
- `"boolean"`
- `"symbol"`
- `"undefined"`
- `"object"`
- `"function"`

#### Boolean

```ts
function printAll(strs: string | string[] | null) {
  if (strs && typeof strs === "object") {
    for (const s of strs) {
      console.log(s);
    }
  } else if (typeof strs === "string") {
    console.log(strs);
  }
}
```

Coerced to false

- `0`
- `NaN`
- `""` (the empty string)
- `0n` (the `bigint` version of zero)
- `null`
- `undefined`

#### instanceof

x instanceof Foo checks whether the *prototype chain* of `x` contains Foo.prototype

```ts
unction logValue(x: Date | string) {
  if (x instanceof Date) {
    console.log(x.toUTCString());
  } else {
    console.log(x.toUpperCase());
  }
}
```

### Advanced Types => Type predicates

##### Way 1

```ts
if ("swim" in pet) {
	return pet.swim();
}
```

##### Way 2

```ts
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}

// Both calls to 'swim' and 'fly' are now okay.
let pet = getSmallPet();
 
if (isFish(pet)) {
  pet.swim();
} else {
  pet.fly();
}
```

