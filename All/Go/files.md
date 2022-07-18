# Files

```go
import (
	"fmt"
	"io"
	"os"
    "io/ioutil"
    "path/filepath"
)
```

## Basics

### Writing

```go
func main() {
    file, err := os.Create("./fromString.txt") //ptr to file that doesn't/might not exist yet
    checkError(err)
    defer file.Close()
    
    ln, err := io.WriteString(file, "Hello there")
    checkError(err)
    
    fmt.Printf("%v characters", ln)
}

func checkError(err error) {
    if err != nil {
        panic(err) //cause stop and display err
    }
}
```

#### Bytes

```go
func main() {
    bytes := []bytes("Hello there") //create byte array
    ioutil.WriteFile("./fromBytes.txt", bytes, 0644) //0644 is permissions
}
```

### Reading 

```go
fileName := "./hello.txt"

content, err = ioutil.ReadFile(fileName) //content is bytearray
checkError(err)
result := string(content)
```

## Dirs

##### Sample Walk

```go
root, _ := filepath.Abs(".") //root is $(pwd)
err := filepath.Walk(root, processPath) //calls ft for each dir&file 

//must have specific ft signature
func processPath(path string, info os.FileInfo, err error) error {
    if err != nil {
        return err //if return none nil error obj, will stop calling processPath
    }
    
    if path != "." {
        if info.IsDir()  {
            fmt.Println("Dirs:", path)
        } 
    }
    
    return nil
}


```

