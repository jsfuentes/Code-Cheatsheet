# Collections

[docs](https://docs.scala-lang.org/overviews/collections/overview.html)

All of the collections come in 2 variants: immutable and mutable. 

				Iterables
	
			/		|		\
	
		Seq 	|    Set	| 	Map
	
	/		\

IndexedSeq | LinearSeq

There are mutable sets, and immutable sets. With immuable's methods returning new collection

## Common Functions on Seq

- .size
- `++` to concenate 
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

### Sequences

#### Array, Lists, Vector, String

Arrays mutable, lists immutable otherwise same 

Vector is a shallow tree with 32 children per node, logbase32 x bigO, usually better than list unless you are using head/tail

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

##### Range

Can be represented as single obj with lower bound, upper bound, and step size

```scala
1 until 5 //1, 2,3 ,4
val s: Range = 1 to 10 by 3 //1,4,7,10
```

### Functions

- forall, exists, filter, map, zip, unzip, flatMap, sum, product, max, min

## Sets

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

