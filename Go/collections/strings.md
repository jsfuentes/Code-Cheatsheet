## Strings

strings.EqualFold(v1, v2) #incase sensitive comparison

v1 == v2

strings.Contains(toInspect, substr)

## More Complex Objs

Must initialize complex objects(beyond strings)

Wrap initialization in make ft

```go
//DONT!!
var m map[string]int //doesn't have place to put data yet
m["key"] = 42 //will panic
//CORRECT
m := make(map[string]int)
```

