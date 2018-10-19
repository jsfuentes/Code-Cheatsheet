## Maps

Create

```go
var states map[string]string
states := make(map[string][string])
```

Get and set

```go
states["CA"] = "California"
california := states["CA"]
```

- if the key does not exist, then the zero of the value type is returned(0 for int, "" for string)

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



