# Strings

Prepending `s` to strings allow usage of `$variable`

```scala
val name = "James"
println(s"Hello, $name")  // Hello, James
```

Prepending `f` to strings allows simple formatted string like `printf`. Follow the `$variable%s` with the %d or %s etc like `printf` 

```scala
val height = 1.9d
val name = "James"
println(f"$name%s is $height%2.2f meters tall")  // James is 1.90 meters tall
```

he raw interpolator is similar to the `s` interpolator except that it performs no escaping of literals within the string. Here’s an example processed string:

```scala
scala> s"a\nb"
res0: String =
a
b
```

Here the `s` string interpolator replaced the characters `\n` with a return character. The `raw` interpolator will not do that.

```scala
scala> raw"a\nb"
res1: String = a\nb
```

### Single '

`'string1` creates a symbol which are interned strings

`'abcd eq 'abcd` will return true, while `"abcd" eq "abcd"`

Real for strings that are more code than they are data, i.e we don't care the order of characters its really just a symbol like using constants for DB_Names basically