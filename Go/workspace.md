# Workspace

Needed to have multi-files and install libs

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

`go install [package name]` will work anywhere and install package

## Packages

All files in a package must use the same *name*

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

