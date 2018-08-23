# Subtyping

## Extending Classes

```scala
abstract class Base {
    def foo = 1
    def bar: Int
}

class Sub extends Base {
    override def foo = 2 //must include override if you are ovveriding soething
    def bar = 3 //override opt here
}
```

## Function Bounds

```
def selection[A <: Animal](a1: A, a2: A): A =
  if (a1.fitness > a2.fitness) a1 else a2
```

Here, “`<: Animal`” is an *upper bound* of the type parameter `A`.

It means that `A` can be instantiated only to types that conform to `Animal`.

Generally, the notation

- `A <: B` means: *A is a subtype of B*, and(upper bound)
- `A >: B` means: *A is a supertype of B*, or *B is a subtype of A*.(lowerbound)

