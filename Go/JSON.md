# JSON

Parsing data from a response

```go
import (
	"encoding/json"
    "strings"
    "fmt"
)
```

### Parsing Into Struct

```go
type App struct {
    Id string `json:"id"`
    Title string `json:"title"`
}

data := []byte(`
    {
        "id": "k34rAT4",
        "title": "My Awesome App"
    }
`)

var app App
err := json.Unmarshal(data, &app)
```

#### Struct => Json

```django
b, err := json.Marshal(m)
```

### Simpler Parsing Into Struct

will need to be same as JSON keys and vals(not case sensitive)

```go
type Tour struct {
    Name, Price string 
}
```

### Printing Byte Array

```go
fmt.print("%s", byt)
```

### Decoder 

Grab json data from content using you struct

```go
func toursFromJson(content string) []Tour { //content is array of JSON
    tours := make([]Tour, 0, 20)
    
    decoder := json.NewDecoder(string.NewReader(content))
    _, err := decoder.Token() //throw away that first '[' 
    checkError(err)
    
    var tour Tour
    for decoder.More() { //More asks if there is another data entity and if true returns true and moves decoder there
        err := decoder.Decoder(&tour)//parse JSON and only get those values in your struct leaving it in tour
        checkError(err)
        tours = append(tours, tour)
    }
    
    return tours
}
```

