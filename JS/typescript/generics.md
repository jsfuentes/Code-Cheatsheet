# Generics

A type that takes other types are parameters

### Limiting Acceptable Types 

extends on the left limits the types acceptable

```typescript
type RecursivePartialBy<T, K extends keyof T> = Omit<T, K> &
  RecursivePartial<Pick<T, K>>;
```

### Conditional Typing

extends on the right can create conditional typing

```typescript
type TypeDataPartial<T> = T extends { type_data: unknown }
  ? RecursivePartialBy<T, "type_data">
  : T;
```

