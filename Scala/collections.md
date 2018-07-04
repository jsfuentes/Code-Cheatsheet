# Collections

[docs](https://docs.scala-lang.org/overviews/collections/overview.html)

All of the collections come in 2 variants: immutable and mutable. There are mutable sets, and immutable sets. Both of them work exactly as you’d expect. i.e.

```scala
val immSet = scala.collections.immutable.Set(1, 2, 3)
val mutSet = scala.collections.mutable.Set(1, 2, 3)
immSet.contains(1) // true
mutSet.contains(2) // true 
```

Imm update methods return new collection

## Common Functions

- .size
- .filter(x => x> 1)
  - remove any elem that X => bool returns false for
  - `val sigTrackTopics = allTopics.filter(topic => topic.sigTrackAvailable()) `
- Foreach 
  - `val stuff = Seq(thing1, thing2, thing3, thing4)stuff.foreach { thing =>  S3.delete(thing)}`
  - better than while cuz list's require indexing(linear) less lines and ez parallelism
  - sideeffects only
- .mkString
  - fancy to string with prefix, separator, suffix
- conversions i.e .toSet 
- .map(p => p * 3)
  - applies transformation to every elem in collection

## Types

#### Array Vs Lists

Arrays mutable, lists immutable otherwise same 

```scala
val fruit: List[String] = List("apples", "oranges", "pears")

fruit.head
fruit.tail
fruit.isEmpty
fruit.size # also length
```

```scala
4::intList //append to list
intList1:::intList2 //concentate list
```

##### I Know its a linked list, but I want to index

```scala
l(2)
l.lift(2) //return None if out of bounds
```

### Sets

### Tuple

```scala
val glazedDonutTuple = Tuple2("Glazed Donut", "Very Tasty")
val hostPort = ("localhost", 80)
val x = 1 -> 2 //(1, 2)
gTuple._1 //1 index => "localhost"
gTuple._2 

hostPort match {
  case ("localhost", port) => ...
  case (host, port) => ...
}
```

### Maps

Functionally list of pairs

```scala
Map("foo" -> "bar")
```

### Option

may or may not hold something, staticallly enforced to check for emptiness

Do `var username: Option[String] = None` isntead of `var username = null`

Basically: 

```scala
trait Option[T] {
  def isDefined: Boolean
  def get: T
  def getOrElse(t: T): T
}
```

Map returns Option

```scala
val x = Some("a string")
val result = Res1.getOrElse(0) * 2 //default 0 

val result = res1 match {
  case Some(n) => n * 2
  case None => 0
}
```

Commonly use map and other such functions

```scala
val someInt = Some (2)
  val noneInt:Option[Int] = None
  val someIntRes = someInt.map (_ * 2) //Some (4)
  val noneIntRes = noneInt.map (_ * 2) //None
```



## Futures

Async collection of at most one thing that may or may not exist yet, commonly you map over it

```scala
val futureHttpResult = WS.url(“http://catpictures.dev/top10”).get()
val webPage = futureHttpResult.map { catPicturesHttpBody =>
  val parsed = parse(catPicturesHttpBody)
  val firstPictureUrl = parsed.get(0)
  Ok(myWebPageTemplate(firstPictureUrl))
}
webPage
```

**Nonblocking** Looks sequential, but when it does load inner map block runs

Promises like syntax

```scala
val fut1: Future[Assignment] = Future(nextAssignmentStore.get(classId1))
val fut2: Future[Assignment] = Future(nextAssignmentStore.get(classId2))
val fut3: Future[Assignment] = Future(nextAssignmentStore.get(classId3))
val allFutures: List[Future[Assignment]] = List(fut1, fut2, fut3)
```

Need Future[List[_]] instead of List[Future[_]]

then runs when all complete

```scala
val allResults: Future[List[Assignment]] = Future.sequence(allFutures)
allResults.map { results =>
  Result(results, paging = None)
}

```

