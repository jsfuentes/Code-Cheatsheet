## Conditional Expressions

def example(x: Int) = if x>=0 x else x

has `assert` built-in

## Pattern Matching

```scala
val times = 1
times match {
  case 1 => "one"
  case 2 => "two"
  case _ => "some other number"
}

//Matching with guards
times match {
  case i if i == 1 => "one"
  case i if i == 2 => "two"
  case _ => "some other number"
}

//Matching on Type
def bigger(o: Any): Any = {
  o match {
    case i: Int if i < 0 => i - 1
    case i: Int => i + 1
    case d: Double if d < 0.0 => d - 0.1
    case d: Double => d + 0.1
    case text: String => text + "s"
  }
}
```

### Case Classes

convenientaly store and match on class contents(i.e insted of if comp.brand == "HP")

```scala
case class Calculator(brand: String, model: String)
val hp20b = Calculator("HP", "20b")
```

ez equality and toString

##### Using with match

```scala
def calcType(calc: Calculator) = calc match {
  case Calculator("HP", "20B") => "financial"
  case Calculator("HP", "48G") => "scientific"
  case Calculator("HP", "30B") => "business"
  case Calculator(ourBrand, ourModel) => "Calculator: %s %s is of unknown type".format(ourBrand, ourModel)
}
```

