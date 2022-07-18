# Functions

Uppercase functions are exported for package

No overloading

```go
func [name]([arg1] [argtype1], ...) [rtype] {
    
}
```

e.g

```go
func addV(val1 int, val2 int) int {
    return val1 + val2
}

sum := addV(1, 4)
```

If all same type can omit types

```go
func addV(val1, val2 int) int {
    return val1 + val2
}
```

#### Arbitrary Amount of Args

Can do if all same type

```go
func addAllValues(values ...int) int { //passes in args as slice
    sum := 0
    for i:= range values {
        sum += values[i]
    }
    return sum
}

addAllValues(45, 123, 7)
```

#### Multi Returns

Neccessary for error handling as often return (val, err)

```go
func FullName(f, l string) (string, int) {
    full := f + " " + l
    return full, len(full)
}
```

#### Naming Returns(Naked Returns)

Don't return, just set vars

```go
func FullName(f, l string) (full string, length int) {
    full = f + " " + l
    length = len(full)
    return 
}
```

## Defer

defer is put on a stack and done in LIFO order at end of ft scope

Uses?

- defer closing of database and files 

```go
func main() {
    defer fmt.Println("C")
    fmt.Println("A")
    defer fmt.Println("B")
} ///=> prints A B C
```

vars have value frozen

```go
func main() {
    x := 1000
    defer fmt.Println("X: ", x) 
    x += 1
    fmt.Println("X: ", x)
} // => 1001 1000
```