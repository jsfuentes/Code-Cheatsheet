# Functions

```scala
def abs = 1
abs + 1
def abs() = 1 
abs() + 1
def abs(x) = x
def abs(x) = { x + 1 }
def +?%&(x) = x //Allowed to have symbols name function
```

```scala
def abs(x: Double):Double = {
    def absHelper() = x
    absHelper()
}

val result = {
    val x = f(3)
    x * x
}
```

#### TAIL RECURSION == LOOPS (Reuse stack space)

- Last action of ft consists of calling another ft 
- ft vs ft * 2
- @tailrec annonation ensures tail recursive

## Anonymous

like javascript 

```scala
x => x * x
//or 
_ * _
```

## Special Arg Types

### CASE match

```scala
def f = { case Keyed(feedbackId, feedback) =>
            Keyed(feedbackId, Feedback.toLearnerView(feedback))
}

//jorge now is given KeyObject
def f = { case jorge @  Keyed(feedbackId, feedback) =>
            Keyed(feedbackId, Feedback.toLearnerView(feedback))
}
```

### Partial Application

```scala
scala> def adder(m: Int, n: Int) = m + n
adder: (m: Int,n: Int)Int
scala> val add2 = adder(2, _:Int)
add2: (Int) => Int = <function1>

scala> add2(3)
res50: Int = 5
```

You can partially apply any argument in the argument list, not just the last one.

### Variable Length Args

```scala
def capitalizeAll(args: String*) = {
  args.map { arg =>
    arg.capitalize
  }
}

scala> capitalizeAll("rarity", "applejack")
res2: Seq[String] = ArrayBuffer(Rarity, Applejack)
```



## Representation 

Recall Int => Int is a function that takes a Int and returns an Int

### Currying

Built in language!

sum takes a function that take ans returns an int and returns a ft that takes two ints and returns an int

```scala
def sum(f: Int => Int): (Int, Int) => Int = {
    def sumF(a: Int, b: Int): Int = 
    	if (a>b) 0
    	else f(a) + sumF(a+1, b)
    sumF
}
//equal to 
def sum(f:Int => Int) (a: Int, b: Int): Int = 
if (a>b) 0 else f(a) + sum(f)(a+1, b)
```

```scala
sumCube = sum(cube)

sumCube(1, 10)

sum(cube)(1, 10)
```

## Generics

```scala
def singleton[T](e: T) = new Cons[T](e, new Nil[T])

singleton(1) //complier infers type
singleton(true)
```

