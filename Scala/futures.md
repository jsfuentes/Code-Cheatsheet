# Futures

Placeholder object for value that may not yet exist, revolve around `ExecutionContext` which has access to a thread pool similar to Executor design pattern

## Defining

```scala
// delegate the execution of fatMatrix.inverse() to an ExecutionContext and embody the result of the computation in inverseFuture.

val inverseFuture: Future[Matrix] = Future {
  fatMatrix.inverse() // non-blocking long lasting computation
}(executionContext)

implicit val ec: ExecutionContext = ...
val inverseFuture : Future[Matrix] = Future {
  fatMatrix.inverse()
} // ec is implicitly passed
```

### Defining Global Execution Context

```scala
//1
import scala.concurrent.ExecutionContext.Implicits.global
//2
implicit val executor =  scala.concurrent.ExecutionContext.global
//3
Future { /* do something */ }(executor)
```



## States

not yet completed, **not completed**

completed with value or exception, **completed**

- **failed** with exception or **successfully completed** with value

Immutable after it becomes completed

## Callbacks

```scala
f onComplete {
  case Success(posts) => for (post <- posts) println(post)
  case Failure(t) => println("An error has occurred: " + t.getMessage)
}
```

Callback takes a `Try[T] => U` where Try[T] is like an option but contains either the variable or an exception

## Combinators

#### Only Success (foreach)

```scala
f foreach { posts =>
  for (post <- posts) println(post)
}
```

#### Change Future Value (map)

```scala
val rateQuote = Future {
  connection.getCurrentValue(USD)
}

val purchase = rateQuote map { quote =>
  if (isProfitable(quote)) connection.buy(amount, quote)
  else throw new Exception("not profitable")
}

purchase foreach { _ =>
  println("Purchased " + amount + " USD")
}
```

exception are propagated

#### For comprehensions(flatmap & withfilter)

flatmap -> like map but ft returns a future not a value, used to call ft's that return future on value yet to be computed

for loop basically allows several flatMaps then a final map yielding a Future value

futures start running immediately on seperate threads and main thread runs through this without blocking

resultF is just a Future that waits for component parts to finish before completing itself

```scala
val threeF = Future(3)
val fourF = Future(4)
val fiveF = Future(5)

val resultF = for{
  three <- threeF
  four <- fourF
  five <- fiveF
}yield{
  three * four * five
}

//EQUALS

val resultF = threeF.flatMap(three => fourF.flatMap(four => fiveF.map(five => three * four * five)))
```

Example 2

```scala
val usdQuote = Future { connection.getCurrentValue(USD) }
val chfQuote = Future { connection.getCurrentValue(CHF) }

val purchase = for {
  usd <- usdQuote
  chf <- chfQuote
  if isProfitable(usd, chf)
} yield connection.buy(amount, chf)

purchase foreach { _ =>
  println("Purchased " + amount + " CHF")
}

//EQUALS

val purchase = usdQuote flatMap {
  usd =>
  chfQuote
    .withFilter(chf => isProfitable(usd, chf)) //throws exception in future if bool false
    .map(chf => connection.buy(amount, chf))
}
```

#### Exception recovery

- recover
- RecoverWith
- fallbackTo

## Coursera Usage

future.flatMap(x =>

​	x

​	...

​	y.flatMap( t =>

​		t

​	)

)



is the same as

x <- future

Thread blocks while the future waits to finish and collapse

y <- x