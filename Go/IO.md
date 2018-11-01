# Fmt

Stdout/in

## Output

`Println` - print with newline

`Print` - print w/out newline 

```go
package main
import "fmt"

func main() {
    str := "Hello"
    str := "Jorge"
    
    stringLength, err := fmt.Println(str1, str2, str3)
    # Prints Hello Jorge
    
    if err == nil {
        fmt.Println("string length:", stringLength)
    }
}
```

**Printf**

`fmt.Printf("value of a Number: %v\n", aNumber)`

got a lot of % stuff like `%T` for type

**Sprintf** is like printf but returns the value

## Input

**Scanf** gets first string 

### buffo/os

```go
package main

import (
	"fmt"
	"bufio"
	"os"
	"strconv"
    "strings"
)

func main() {
    reader := bufio.newReader(os.Stdin)
    fmt.Print("Enter text: ")
    str, _ := reader.ReadString('\n') #read string
    fmt.Println(str)
    
    fmt.Print("Enter a number: ")
    str, _ = reader.ReadString('\n') 
    trimStr := strings.TrimSpace(str) # read and parse float
    f, err := str.conv.ParseFloat(trimStr, 64)
    if err != nil {
        fmt.Println(err)
    } else {
        fmt.Println("Value of number:", f)
    }
}
```

## Advanced Formatin

| Modifer | Description                     |
| ------- | ------------------------------- |
| %06d    | Print with width 6, pad with 0s |
| %s      | Print as string                 |
| %T      | Type                            |

