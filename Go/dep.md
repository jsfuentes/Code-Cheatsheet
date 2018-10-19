# Go Get Vs Dep

- go get more for consumers of go code
- dep for developers to manage version and the like

## Go Get

### Installation 

`go get github.com/tensorflow/tensorflow/tensorflow/go`

Fetch, build, and install remote package into workspace defined by $GOPATH \

### Usage

```go
package main

import (
    tf "github.com/tensorflow/tensorflow/tensorflow/go" //access with tf.
    "github.com/tensorflow/tensorflow/tensorflow/go/op" //access with op.
    "fmt"
)

func main() {
    // Construct a graph with an operation that produces a string constant.
    s := op.NewScope()
    c := op.Const(s, "Hello from TensorFlow version " + tf.Version())
}
```

