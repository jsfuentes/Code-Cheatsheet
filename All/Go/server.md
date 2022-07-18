# Simple Server

```go
import (
	"fmt"
	"net/http"
)
```



## Serving

Have a struct that has a func, ServeHTTP will be called to service requests

```go
type Hello struct {}

func (h Hello) ServeHTTP(w http.ResponseWriter, r *http.Request) { 
    fmt.Fprint(w, "<h1> Hello from Go </h1>")//print to writer object
}
```

#### Usage

```go
func main() {
    var h Hello
    err := http.ListenAndServe("localhost:4000", h)
    checkError(err)
}
```

