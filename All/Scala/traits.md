# Traits

Interface like `traits` are fields and behaviors that you add to classes

Better than Java interfaces b/c offers value parameters and methods

```scala
trait Car {
  def two: Int = 1 * 2 
  val brand: String 
}

trait Shiny {
  val shineRefraction: Int
}
```

### Extending Traits

```scala
class BMW extends Car {
  val brand = "BMW"
}
```

One class can extend several traits using the `with` keyword:

```scala
class BMW extends Car with Shiny {
  val brand = "BMW"
  val shineRefraction = 12
}
```

-better than abstract classes cuz can extend multiple traits 

- can't have abstract class constructors, or import in Java as easily

