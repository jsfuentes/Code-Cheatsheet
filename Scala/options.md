## Option

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

