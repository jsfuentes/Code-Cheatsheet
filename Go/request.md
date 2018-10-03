# Request

```go
import (
	"fmt"
	"net/http"
    "io/ioutil"
)
```

Get returns http.Response

```go
resp, err := http.Get(url)
checkErr(err)

fmt.Printf("Response type: %T\n", resp) 
```

### Work with Data

```go
resp, err := http.Get(url)
checkErr(err)

defer resp.Body.Close()

bytes, err := ioutil.ReadAll(resp.Body)
checkErr(err)

content := string(bytes) 
```

