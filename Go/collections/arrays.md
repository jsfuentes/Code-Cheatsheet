## Arrays

```go
var colors [3]string
fmt.Println(colors)
fmt.Println(colors[1])

var numbers = [5]int{5,3,1,2,4}
```

### Slice

Abstraction on top of array, resizable and sortable

Can use base array stuff 

```go
var colors = []string{"Red", "Green", "Blue"} //w/out number its a slice

colors = append(colors, "Purple") 
colors = append(colors[:len(colors) - 1])//python slicinggg
//colors removed first item
```

**Make** ([type], [initial size], [capacity or inital size]): allocate & initialize

**New**: allocates but !initialize mem, if you try to set val you fail 

```go
numbers := make([]int, 5, 5)
cap(numbers) //=> 5
//.... add 5 numbers
numbers = numbers.append(numbers, 235)
fmt.Println(cap(numbers)) //=> 10 ; check new capacity
```

- `sort.Ints(numbers)` with `sort` package

## 