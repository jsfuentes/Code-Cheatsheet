# Fun

Semicolon optional unless multiple statements on same line

## Main

```scala
object session extends App {
    println("Hello world")
}

object session {
    def main {
        println("Hello world")
    }
}
```

## Evaluation Rules

- Call by value: evaluates the function arguments before calling the function
- Call by name: evaluates the function first, and then evaluates the arguments if need be

```scala
def example = 2      // evaluated when called
val example = 2      // evaluated immediately
lazy val example = 2 // evaluated once when needed

def loop = loop //won't loop forever at this line
val loop = loop //will loop forever at this line

def square(x: Double)    // call by value
def square(x: => Double) // call by name
def myFct(bindings: Int*) = { ... } // bindings is a sequence of int, containing a varying # of arguments
```

# Functions

Blocks {....}, expression

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

## Lists

```scala
val fruit: List[String] = List("apples", "oranges", "pears")

fruit.head
fruit.tail
fruit.isEmpty
```

```scala
4::intList //append to list
intList1:::intList2 //concentate list
```

## Conditional Expressions

def example(x: Int) = if x>=0 x else x