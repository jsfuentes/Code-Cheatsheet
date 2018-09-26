# Errors

Err is interface that implements a single ft that return string

```go
f, err := os.Open("filename.txt")
if err == nil {
    fmt.Println("f")
} else {
    fmt.Println(err)
    //SAME AS
    fmt.Println(err.Error())
}
```



## Creating Errors

```go
import (
	"errors"
)

myError := errors.New("My error string")
```

### Other Examples

```go
attendance := map[string]bool {
    "ann": true,
}
attended, ok := attendance["M"]
if ok {
    fmt.Println("M?", attended)
} else {
    fmt.Println("No info")
}
```

