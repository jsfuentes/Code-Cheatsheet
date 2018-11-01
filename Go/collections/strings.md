## Strings

```go
import (
    "strings"
	"strconv"
)
```

`'c'` single quotes for characters

`"str"` double quotes for strings

#### Equality

strings.EqualFold(v1, v2) #case insensitive comparison

v1 == v2

## String Functions

| Function                                | Example                       |
| --------------------------------------- | ----------------------------- |
| strings.Contains([toInspect], [substr]) | strings.Contains("aba", "ab") |
| strings.Split(toSplit, split)           | strings.Split("12.03", ":")   |
|                                         |                               |

strings.Contains(toInspect, substr)

strings.Split(toSplit, split)

## Conversions

```go
i, err := strconv.Atoi("-42")
s := strconv.Itoa(-42)
```

## More Complex Objs

Must initialize complex objects(beyond strings)

Wrap initialization in make ft

```go
//DONT!!
var m map[string]int //doesn't have place to put data yet
m["key"] = 42 //will panic
//CORRECT
m := make(map[string]int)
```

