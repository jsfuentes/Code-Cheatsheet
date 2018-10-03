# Control

If you end with a complete statement, lexer puts `;`  so `{`/`else` must be on same line

## If

```go
if x < 0 {
	result = "Greater"
} else if x == 0 {
    result = "Equal"
} else {
    result = "Less"
}
```

### Scoping

Can scope to conditonal block 

```go
if x := 42; x < 0 {
    //....
}
fmt.Println(x) //WONT WORK
```

## Switch

Like C/Java, but evaluates any simple type and no breaks needed jumps after block fround

```go
//switch dow {
switch dow := rand.Intn(6); dow {
    case 1:
        //..
    case 7:
        //..
    default:
        //..
}
```

Can do if like stuff

```go
x := -42;
switch {
    case x > 0:
    	result = "Greater"
    case x < 0:
    	result = "Less"
    	fallthrough //execute everything below too
	default:
    	result = "Equal or Less"
}
```

## For

##### Basic

```go
for i := 0; i < 10; i++ {
    sum += i
}
```

##### Over a collections

```go
for i := 0; i < len(colors); i++ {
    fmt.Println(colors[i])
}

for i := range colors { //set i to current index	
    fmt.Println(colors[i])
}
```

##### While

```go
for sum < 1000 {
    sum += sum
    if sum > 500 {
        break
    }
}
```

## GO-TO!!!

with labels and jumps

```go
endofprogram : fmt.Println("start of program")

if sum > 200 {
    sum -= sum
    goto endofprogram
}
```

