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

## Panic, Defer, and Recover

#### Defer

Puts a func on the call stack that will be run in reverse order when host ft finishes 

```go
resp, _ := http.Get("http://golang.org")
defer func () {
   if resp != nil {
      resp.Body.Close()
   }
}()
body, _ := ioutil.ReadAll(resp.Body)
```

#### Panic

stops execution passing control to deferred fts

```go
func panic(v interface{}) 
```

#### Recover

Only available in a defer, catch a panic 

```go
func Perform() (err error) {
   defer func() {
      if r := recover(); r != nil {
         err = r.(error)
      }
   }()
   GoesWrong()
   return
}
func GoesWrong() {
   panic(errors.New("Fail"))
}
func main() {
   err := Perform()
   fmt.Println(err)
}
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

