# Dates

Time package

Package

- `.Now()`

Object

- `.Month()`, `.Day()`, `.Weekday()`
- `.addDate(0, 0, 1)

```go
package main

import (
	"fmt"
	"time"
)

func main() {
    t := time.Date(2009, time.November, 10, 23, 0, 0, 0, time.UTC)
    fmt.Printf("Go launched at %s\n", t)
    
    now := time.Now()
    
}
```

## Creating your format

Based on Jan 2nd 3rd hours 4 minute 5 second and 6 year and -7 Time zone

```go
longFormat  := "Monday, Janurary 2, 2006"
shortFormat := "1/2/06"
fmt.Println("Tomorrow is", time.Now().Format(longFormat))
```



