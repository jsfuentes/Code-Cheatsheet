# Go

Playground: [play.golang.org](play.goland.org)

## Overview

- Compiled exec OS specific and have statically linked runtime(contains all needed libs)
- Custom types can implement interfaces and have methods
- Custom structs have member fields
- GO's class with no inheritance, no constructors, no generics(operator overloading), no exception handling, no implicit numeric conversions
- Next-gen succient C 
- Garbage Collection, mem reclaimed when objects out of scope of set to nil very fast
- Scopes to blocks 
- Great concurrency(Goroutine, channel, select) 

#### CLI

`go run [file]`

`go build [file]`

`godoc [package]` ie. `godoc fmt` gives you all exported functions and comments

`gofmt -w [file]`  To override and format file

## Hello World

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

Exported fts and fields have initial upper-case character

starting brace must be on same line

*builtin* package

