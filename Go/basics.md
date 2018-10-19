# Basics

Lexer puts semicolon if complete statement i.e must put { on same line as if and else on same line as }

Must explicitly change types for everything

```go
package main

import(
  "fmt"
  "strings"
)

func main() {
  fmt.Println("Hello from Go!")
  fmt.Println(strings.ToUpper("Hello really loud"))
}
```

## Types

- bool, string
- uint8, int8, 16, 32, byte
- float32, float64, complex32
- uint, int(change on os)
- functions, interfaces, channels
- ptrs
- arrays, slices, maps, structs

Explicit or implicit typing

*Same logical operators as C/C++)*

### Declare

```go
var aInt int 
var s string
```

Unintialized vars are given a default value(0 for int, "" for string)

### Explicit =

```go
var aInt int = 42
var aStr string = "this is go!"
const aInt int = 42
```

### Implicit :=

```go
aInt := 42
aStr := "This is go!"
const aStr = "This is Go!"
i1, i2, i3 := 12, 45, 241
```

**Future assignment use = **

## Ptrs

Basically C ptrs

```go
var p *int 
*p // to get val 
if p != nil {
    fmt.Println("P: ", *p)
}


p = &v1 //& get ref
```

## Panic

Cause program stop and can pass in err to display

```go
func checkError(err error) {
    if err != nil {
        panic(err) 
    }
}
```

