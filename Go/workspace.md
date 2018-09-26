# Workspace

Needed to have multi-files

## Setup

Make the following dir struct:

[folder]

​	bin #for exec

​	pkg #for intermediate

​	src 

​		[package name]

​			[filename].go

Then `export GOPATH=[folder path]`

Startup file has `package main` at top and a `func main`

Now `go install` in the [package name] folder will create stuff in bin

## Packages

under src>stringutil>stringutil.go

```go
package stringutil

func FullName(s, l) {
    //....
}
```

In other package

```go
package main

import (
	"stringutil"
)

func main() {
    author := stringutil.FullName("Jorge", "Fuentes")
}
```

