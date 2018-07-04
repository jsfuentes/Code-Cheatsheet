# Scala

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

## Basic Defining Blocks 

- Call by value: evaluates the function arguments before calling the function

- Call by name: evaluates the function first, and then evaluates the arguments if need be

```scala
def example = 2      // evaluated when called
val example = 2      // evaluated immediately and immutable
var exmaple = 2 //variable and immediate
lazy val example = 2 // evaluated once when needed

def loop = loop //won't loop forever at this line
val loop = loop //will loop forever at this line

def square(x: Double)    // call by value
def square(x: => Double) // call by name
def myFct(bindings: Int*) = { ... } // bindings is a sequence of int, containing a varying # of arguments
```

## Expressions

the building block of scala

Blocks {} are an expression that returns the last expression's value. so can be stored in variables returned by functions and be parameters

```scala
var y = 2		//variable	
val x = 1		//immutable
```

## Basic Types

"" - strings

'' - chars 



##  Packages

place at top to declare everything as file

```scala
package com.twitter.example
```

Instead of importing `*` import `_` i.e`import scala.collections.JavaConversions._` 

## Try Catch

```scala
//val result: Int = //an expression so can do this
try {
  remoteCalculatorService.add(1, 2)
} catch {
  case e: ServerIsDownException => log.error(e, "the remote calculator service is unavailable. should have kept your trusty HP.")
} finally {
  remoteCalculatorService.close()
}
```

