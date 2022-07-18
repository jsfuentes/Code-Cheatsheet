# TypeScript
A superscript of javascript that is transpiled into javascript. Even if an error, will compile to javascript. I.e using the wrong type for a variable will produce compile error, but produce working js
New:

* Strong Typing
* Object oriented
* Compile time errors

Valuable Because:

- Get types from librarys to see all options and info in IDE
- Much more static type errors especially around null checks
- Easier to use internal code with argument annotations

## Type Files

Types packages should just be in [devDependencies](https://stackoverflow.com/questions/45176661/how-do-i-decide-whether-types-goes-into-dependencies-or-devdependencies)

Should have `.d.ts` extension as recommended

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

