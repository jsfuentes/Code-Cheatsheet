## Maps

Create

```go
var states map[string]string
states := make(map[string]string)
commits := map[string]int{
    "rsc": 3711,
    "r":   2138,
    "gri": 1908,
    "adg": 912,
}
```

Get and set

```go
states["CA"] = "California"
california := states["CA"]
cal, ok := s["CCCC"] //opt ok 
```

- if the key does not exist, then the zero of the value type is returned(0 for int, "" for string) and ok is false

Delete

```go
delete(states, "CA") //[]
```

Iterate

```go
for k, v := range states {
    fmt.Printf("%v, %v\n", k, v)
}
```

List 

```go
key := make([]string, len(states))
i := 0
for k := range states {
    keys[i] = k 
    i++
}
```



