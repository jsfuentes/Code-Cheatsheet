# Loops

```scala
for( var x <- Range ){
   statement(s);
}

 for( var a <- 1 to 10){
     println( "Value of a: " + a );
 }
```

## Ranges

```scala
i to j // includes j
i until j //excludes j
```

Can use multiple ranges separate by `;` and will iterator over al combos of both

```scala
for( a <- 1 to 3; b <- 1 to 3){
    println( "Value of a: " + a );
    println( "Value of b: " + b );
}
```

(1, 1) -> (1, 2) -> (1, 3) -> (2, 1) -> ...

## Containers

Can also be containers

```scala
val numList = List(1,2,3,4,5,6);

// for loop execution with a collection
for( a <- numList ){
    println( "Value of a: " + a );
}
```

## With Filters/Guards

can filter out with if in for loop

```scala
for( a <- numList
    if a != 3; if a < 8 ){
    println( "Value of a: " + a );
}
```

## With Yield

Creates a new data structue from an existing one

```scala
val names2 = for (e <- names) yield e.capitalize
val lengths = for (e <- names) yield {
    // imagine that this required multiple lines of code
    e.length
}
```

