# Arrays

Fixed Length

#### Creation

```go
var colors [3]string
var numbers = [5]int{5,3,1,2,4}
names := [...]string{1,2,3,4,5,6,7,8,9}//... counts number 
```

#### Usage

```go
colors[:len(colors) - 1] //python slicinggg 
fmt.Println(colors)
fmt.Println(colors[1])
```

## Slice

Abstraction on top of array, has make capacity

Struct with ptr passed by value, so array reference passed by ref and length pass by val

Can use base array stuff 

#### Initialization

**Make** ([type], [initial size], [capacity or inital size]): allocate & initialize

**New**: allocates but !initialize mem, if you try to set val you fail 

W/out number its a slice

- `var x []float64` //length 0
- `numbers := make([]int, 5, 5)`
- `var colors = []string{"Red", "Green", "Blue"} `

#### Usage

Append creates a new slice if needed

- `colors = append(colors, "Purple") `
- `sort.Ints(numbers)` with `sort` package
- `copy(newSlice, slice)`