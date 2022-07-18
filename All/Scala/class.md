# Class 

All Scala classes are derived from Object(from Java)

## Declaration

```scala
class Rational(x: Int, y: Int) {
    require(y > 0, "y must be positive") //basically assert but different exception
    
    def numer = x
    def denom = y
    private val g = 3
    
    def this(x: Int) = this(x, 1) //constructor overloading
    
    override def toString = "X: " + x + " Y: " + y
    private[this] def myF() {
        //.....
    }
}
```

### Usage 

```scala
val x = new Rational(1, 2)
x.numer
x.denom
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

## Class Modifiers

### abstract

cant be instated with new and can have unimplemented its

```scala
abstract class Shape {
    def getArea():Int// subclass should define this
}		
```

### Sealed & Final

`final` can't be extended anywhere and `sealed` can only be extended in the same Scala file

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

