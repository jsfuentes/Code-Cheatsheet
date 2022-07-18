## Interfaces

No keyword like extends, if you implement all the methods then you can be that type

So everything is the empty `interface{}`

```go
type Animal interface {
    Speak() string
}
```

### Usage

```go
type Dog struct {
    //...
}

func (d Dog) Speak() string {
    return "Woof"
}

func main() {
    poodle:= Animal(Dog()) //cast as Animal
}
```

## The empty interface

- Specifies no methods
- May hold values of any type like fmt.Println

```
interface{}
```

An empty interface may hold values of any type. (Every type implements at least zero methods.)