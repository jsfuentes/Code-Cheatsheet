# Class 

## Declaration

```scala
class Rational(x: Int, y: Int) {
    require(y > 0, "y must be positive") //basically assert but different exception
    
    def numer = x
    def denom = y
    private val g = 3
    
    def this(x: Int) = this(x, 1) //constructor overloading
}
```

### Usage 

```scala
val x = new Rational(1, 2)
x.numer
x.denom
```

### abstract

```scala
abstract class Shape {
    def getArea():Int// subclass should define this
}		
```

## Case Classes

convenientaly store and match on class contents(i.e insted of if comp.brand == "HP")

Basically extras on top of class that can be used like a class

```scala
case class Calculator(brand: String = "Dell", model: String) //Dell default
val hp20b = Calculator("HP", "20b") //without new keyword
```

- Getters, no setters
- generates hashcode, toStr, and equals
- ez copying `hp20b.copy(brand = "Texas")`

## Traits

Interface like `traits` are fields and behaviors that you add to classes

```scala
trait Car {
  val brand: String
}

trait Shiny {
  val shineRefraction: Int
}
```

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

## Objects

- Basially singleton class(can have object and class with same name; often for factories)

- Define with `object` instead of `class` and be able to use instantly

## Generics

```scala
trait Cache[K, V] {
  def get(key: K): V
  def put(key: K, value: V)
  def delete(key: K)
}
```

## Ez Overloading

#### Usage

```scala
r.add(s)
//if one parameter
r add s 
```

Soooo you can have very natural operator overloading on +

```scala
r.-(s)
r - s
```

precedence defined as first character so ez i.e a+b*c == a+(b\*c) regardless of what a, b, and c are 

## Variance

Basically allows you to answer question if B is subclass of A is Container[B] a subclass of Container[A]

Look up more if you need this