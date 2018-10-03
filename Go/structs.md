# Structs

No inheritance 

```go
type Dog struct {
    Breed string 
    Weight int
}

type Cat struct {
}
```

##### Creation

```go
poodle := Dog{"Poodle", 34}
jaguar := Cat{}
```

##### Printing

```go
fmt.Println(poodle) //outputs "Poodle 34" 
fmt.Printf("%+v", poodle) //outputs {Breed:Poodle Weight:34}
```

## Methods

After declaring a type as above

```go
type Dog struct {
	Sound string 
}

//recieves Dog;; pass by val
func (d Dog) Speak() {
    fmt.Println(d.Sound)
}

//pass d by ref
func (d *Dog) doubleDog() {
    d.Sound = fmt.Sprintf("%v! %v!\n", d.Sound, d.Sound) 
    fmt.Print(d.Sound)
}
```

## Interfaces

No keyword like extends, if you implement all the methods then you can be that type

- Everything implents at least one interface, interface() is empty interface that obv everything is

### 

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

